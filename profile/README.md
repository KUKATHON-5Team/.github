
### <p>노인 분들을 위한 알바몬 '내일' !</p>
<div align=center>
<img src="https://user-images.githubusercontent.com/99026631/227742842-0da7d409-e84a-482b-8609-25fcaa07c2a0.png"/>
 
</div>


## Production
http://kukathon-5team.s3-website.ap-northeast-2.amazonaws.com/



***

### 서비스 구조
<img src="https://user-images.githubusercontent.com/99026631/227745222-0a951744-b629-4e15-a68a-402d96d04593.png" width="800px"/>

### 서비스 플로우
<img src="https://user-images.githubusercontent.com/99026631/227745248-e3e4ea6e-8a6b-45c6-a043-a17ecb1f44a1.png" width="800px"/>




***
# Features

## 일자리 찾기
<img src="https://user-images.githubusercontent.com/99026631/227745337-5071a838-2fbf-48ac-bfb9-dd4638b304f0.png" width="400px"/>
자기 자신에게 맞는 일자리 찾기

## 일자리 리스트 업
<img src="https://user-images.githubusercontent.com/99026631/227745393-e49c9144-0ae7-4527-8bc2-e0eb43c32d03.png" width="400px"/>
자기 자신에게 맞는 일자리 리스트 업

## 스트랩 기능
<img src="https://user-images.githubusercontent.com/99026631/227745433-f9dc10a7-0a7e-4e79-b2ad-f5a82b3369f2.png" width="400px"/>
<br/>
자기가 관리하는 노인분들 스트랩

## 상세 페이지
<img src="https://user-images.githubusercontent.com/99026631/227745453-19721f9c-dfa8-4417-8040-2d3415bf15f3.png" width="400px"/>
<br/>
자신이 고른 일자리 상세 보기




***
## Tech Stack

<div align =center>

Area| Tech Stack|
:--------:|:------------------------------:|
**Frontend** | <img src="https://img.shields.io/badge/react-61DAFB?style=for-the-badge&logo=react&logoColor=black"> <img src="https://img.shields.io/badge/html5-E34F26?style=for-the-badge&logo=html5&logoColor=white"> <img src="https://img.shields.io/badge/css-1572B6?style=for-the-badge&logo=css3&logoColor=white">   <img src="https://img.shields.io/badge/javascript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black"> <img src="https://img.shields.io/badge/styledcomponents-DB7093?style=for-the-badge&logo=javascript&logoColor=black"> <img src="https://img.shields.io/badge/S3-569A31?style=for-the-badge&logo=Amazon S3&logoColor=white">
**Backend** |   <img src="https://img.shields.io/badge/spring-6DB33F?style=for-the-badge&logo=spring&logoColor=white">   <img src="https://img.shields.io/badge/java-007396?style=for-the-badge&logo=java&logoColor=white">  <img src="https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white"> <img src="https://img.shields.io/badge/rds-527FFF?style=for-the-badge&logo=mysql&logoColor=white"> 
**DevOps** |  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white"> <img src="https://img.shields.io/badge/Github_Actions-2088FF?style=for-the-badge&logo=Github-Actions&logoColor=black"> <img src="https://img.shields.io/badge/Amazon_EC2-FF9900?style=for-the-badge&logo=Amazon-EC2&logoColor=black">

</div>

***

<details>
<summary> <h3>Front-end</h3></summary>
 
- 근무 조건 선택, 공고 리스트, 상세 정보 반환 페이지 구현
 
- 상세 지역 선택, 스크랩, 서비스 대상 선택 모달창 구현
 
- 카카오 API 연동을 통해 조건 선택에 부합하는 공고 리스트와 지도를 화면에 반환
 
- AWS S3로 정적 배포 후 Github action을 통해 main 브랜치에 Pull Request를 트리거로 CI/CD
 
</details>

<details>
<summary> <h3>Back-end </h3></summary>

- 지역(시,동,구), 직종, 재택여부, 근무기간 조건을 가지고 동적 쿼리를 통해 해당 조건에 부합하는 공고 리스트 반환
 
- 공고 리스트에서 특정 공고를 클릭하면 상세 정보 반환

### ERD

<img src="https://user-images.githubusercontent.com/99026631/227744772-935a4e0b-08ec-4a91-8b33-b5e2f5c4a129.png" width="400px"/>

### Trouble Shooting

- Spring security를 이용해서 로그인 기능을 구현하려 했으나, 프론트와 백엔드 서버가 분리되어있었고 최신 Chrome 환경에서 쿠키를 설정하기 위해서는 Same-Site = none, Secure = true 설정이 들어가야 했습니다. 그래서 쿠키 설정을 변경하였으나 백엔드 서버로 https요청을 보낼때만 쿠키값이 설정이 되어서 백엔드 서버를 nginx, ssl을 통해 https 요청을 받을려고 했습니다. 하지만 ssl 인증서를 받기위해서는 도메인을 가지고 있어야했기에 결국에는 프로젝트에서 로그인 기능을 제외하고 구현하였습니다.
 
- 조건이 4개이고 어떤 조건에는 값이 넘어오지 않을 수 있는 상황에서 Spring Data Jpa가 기본으로 제공해주는 Criteria을 사용하기에는 Criteria는 팀원들이 이해하기 힘든 코드를 만들기 쉬웠기에 과감하게 QueryDsl을 도입했습니다.  기존 동적쿼리를 생성하는 과정을 Method Chaining을 통해 쉽게 관리하였고 특히 조건을 필터링하는 Where 문에 각 조건에 맞는 메서드를 재정의하는 즉 리팩터링 과정을 통해 팀원들이 이해하기 쉬운 코드를 만들었습니다.

</details>

*** 

## Our Team

| Name    | <center>김정우</center>|<center>임지은</center>  | 
| ------- | --------------------------------------------- | ------------------------------------ | 
| Profile | <center> <img width="110px" height="110px" src="https://avatars.githubusercontent.com/u/70098708?v=4" /> </center>|<center><img width="110px" height="110px" src="https://avatars.githubusercontent.com/u/104711336?v=4" /></center>|
| role    | <center>Frontend</center>   | <center>Frontend</center>    | 
GitHub | <center>[@jwo0o0 Kim](https://avatars.githubusercontent.com/u/70098708?v=4)</center> | <center>[@Imjieunn](https://github.com/Imjieunn) </center>| 



| Name    | <center>심규민</center> | <center>박영식</center> | 
| ------- | --------------------------------------- | --------------------------------------- | 
| Profile |<center><img width="110px" height="110px" src="https://avatars.githubusercontent.com/u/73809814?v=4" /></center>|<center><img width="110px" height="110px" src="https://avatars.githubusercontent.com/u/99026631?v=4" /></center>|
| role    | <center>Bakcend </center> | <center>Backend<center> | 
GitHub | <center>[@Sim-km](https://github.com/tlarbals824)</center> | <center>[@0sik](https://github.com/0sik) </center>| 

