# AutoSpot Hands-On Guideline on Tech Friday

> ## AutoSpot 서비스 사용을 위한 AWS Account 계정연결   
<h3><details><summary>Step 1. Cost Management > AutoSpot 메뉴 클릭</summary>
 
 ![cm_autospot_menu](https://user-images.githubusercontent.com/60588746/73699880-5ba49c80-4728-11ea-95e0-dee85714d591.png) 

</details>
</h3> 

<h3>
<details>
 <summary>Step 2. 계정 추가 버튼 클릭</summary>

![btn_add_account](https://user-images.githubusercontent.com/60588746/73699957-8989e100-4728-11ea-9847-9039da73f508.png)


</details> 
</h3>

<h3>
<details>
 <summary>Step 3. CloudFormation 사용 탭으로 연결계정 추가</summary>

    1. 템플릿 열기 
    2. 연결할 AWS Account 계정에 해당되는 IAM User 로 로그인
    3. 스택생성 동의 후 스택생성 클릭  
     
![Approve](https://user-images.githubusercontent.com/60588746/73698971-edf77100-4725-11ea-8686-31077386feb5.png)

    4. 출력 탭에서 값 복사

![autospot_role_arn](https://user-images.githubusercontent.com/60588746/73699396-087e1a00-4727-11ea-8f9e-1f0d39649cdf.png)


    5. 역할 ARN 복사 후 붙여 넣기 후 추가 버튼 클릭 후 계정등록 계속 진행

![paste_role_arn](https://user-images.githubusercontent.com/60588746/73699692-d15c3880-4727-11ea-9f3a-badf5cc37dcd.png)
</details> 
</h3>

<h3>
<details>
 <summary>Step 4. 연결 계정목록 확인</summary>

![account_list](https://user-images.githubusercontent.com/60588746/73700081-eb4a4b00-4728-11ea-86ff-12d450002697.png)

</details> 
</h3>

<h3>
<details>
 <summary>Step 5. 연결계정별 AutoSpot 관리콘솔 진입</summary>

    1. 관리할 연결 계정을 목록에서 클릭
    2. 관리콘솔 화면 이동 후 초기화면 확인

![autospot_entry](https://user-images.githubusercontent.com/60588746/73700080-eb4a4b00-4728-11ea-9d93-b58651a79b68.png)

</details> 
</h3>
</h3>

___

> ## Spot Analyzer 를 통한 Stateless Elastigroup 생성
<h3>
 <details>
 <summary>Step 1. 사전 환경 구성</summary>  

* <details>
    <summary>AWS 관리 콘솔 이용하기</summary> 


   * [AWS Console Link](https://aws.amazon.com/console/) 로그인 후 진행
     * Application Load Balancer 생성
       * [공식가이드참조](https://docs.aws.amazon.com/ko_kr/elasticloadbalancing/latest/application/create-application-load-balancer.html)
     * Auto Scaling Group 생성
       * [공식가이드참조](https://docs.aws.amazon.com/ko_kr/autoscaling/ec2/userguide/create-asg-ec2-wizard.html)
     * Auto Scaling Group을 Load Balancer 에 연결
       * [공식가이드참조](https://docs.aws.amazon.com/ko_kr/autoscaling/ec2/userguide/attach-load-balancer-asg.html)

    </details>

* <details>
    <summary>AWS CLI 이용하기</summary> 

    * Git 설치 
      *  Mac  
           * Step 1 – Homebrew 설치
             * Terminal 윈도우에서 다음 명령어 실행  
               `$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`       
               `$ brew doctor`      
           * Step 2 – Git 설치
               * Terminal 윈도우에서 다음 명령어 실행  
               `$ brew install git"`
      *  Windows
          * Step 1 – [Chocolatey 설치](https://chocolatey.org/docs/installation)
            * 관리자 권한으로 cmd.exe 또는 powershell.exe 실행
              * 다음 명령줄 복사 후 붙여넣고 실행
                * cmd.exe 사용시  
                  * `@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command " [System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"`       
                  
                * powershell.exe 사용시  
                
                  * `Get-ExecutionPolicy` 실행 결과 값이 `Restricted` 인경우 
                    `Set-ExecutionPolicy AllSigned` 또는 `Set-ExecutionPolicy Bypass -Scope Process` 실행.

                  * `Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`
              
              
          * Step 2 – Git 설치
              * Terminal 윈도우에서 다음 명령어 실행  
               `choco install git` 
              



    * AWS CLI 설치 
      * AWS 공식 가이드 참조 
          * [MAC](https://docs.aws.amazon.com/cli/latest/userguide/install-macos.html)  
          * [Windows](https://docs.aws.amazon.com/cli/latest/userguide/install-windows.html)

    * AWS Configure 구성 
      * Terminal Window 에서 다음 명령어 실행 후 ACCESS_KEY, SECRET_ACCESS_KEY, Default Region 입력. 
        * `$ aws configure`
        * ![aws_configure](https://user-images.githubusercontent.com/60588746/74112543-f1d13a80-4be0-11ea-9872-316d936b4abd.png)
  
      
    
    * 제공된 스크립트로 Application Load Balancer, Target Group, Listener, AutoScalingGroup 생성하기  
      * `$ git clone https://github.com/BespinGlobal-KimYeongSeok/autospot-hands-on-tech-friday`  
      * `$ cd autospot-hands-on-tech-friday/asg-alb-listener-targetgroup`  
      * `$ ./create_alb_targetgroup_asg.sh`  

    </details>

</details> 
</h3>


<h3>
 <details>
 <summary>Step 2. Spot Analyzer 로 Discover & Clone </summary>

  
  * Additional Service > Spot Analyzer 들어가기
    * ![spot_analyzer_menu](https://user-images.githubusercontent.com/60588746/74618357-b56b8480-5174-11ea-81b2-4e43dd83742c.png)
  
  * Rediscover Resources 로 생성한 자원 발견하기
    * ![rediscover](https://user-images.githubusercontent.com/60588746/74618691-2c554d00-5176-11ea-890d-b988cd02bfb2.png)

  * 발견된 AutoScalingGroup 클론하기
    * ![clone_asg](https://user-images.githubusercontent.com/60588746/74618453-33c82680-5175-11ea-97aa-36f772624eca.png)

  * 리전과 이름 확인 후 Next 버튼 클릭
    * ![next_clone_asg](https://user-images.githubusercontent.com/60588746/74618569-c9fc4c80-5175-11ea-94ae-30cea67aab7b.png)

  * Elastigroup 요약정보 확인
    * ![summary](https://user-images.githubusercontent.com/60588746/74618572-cc5ea680-5175-11ea-87fd-624e648c1e10.png)

  * Elastigroup 생성 성공 확인
    * ![create_success](https://user-images.githubusercontent.com/60588746/74618575-cec10080-5175-11ea-81fc-5690d56e04b3.png)

</details> 
</h3>

<h3>
 <details>
 <summary>Step 3. Elastigroup 확인  </summary>

  * Elastigroup 상세정보확인
    * ![elastigroup_created](https://user-images.githubusercontent.com/60588746/74618630-fca64500-5175-11ea-998a-672047c9b4d8.png)

</details> 
</h3>






___ 