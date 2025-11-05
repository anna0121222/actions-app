# 코리아 IT 아카데미 국비과정

## CI/CD
### Docker(컨테이너 기반 가상화 기술)
Docker는 애플리케이션을 컨테이너라는 표준화된 단위로 패키징하여 개발부터 테스트, 배포까지 모든 환경에서 일관되고 안정적으로 실행할 수 있게 하는 컨테이너 기술이다.
<br><br>

### Docker 주요 개념
<ul><li><strong>Image</strong>
<br>: 컨테이너를 만들기 위한 실행 환경의 설계도이다.
코드, 라이브러리, 설정 등이 모두 포함되어 있어 이 이미지를 기반으로 언제든 컨테이너를 만들 수 있다.
</li></ul>
<br>

<ul><li><strong>Container</strong>
<br>: 이미지를 실제로 실행한 실행 단위이다.
여러 개의 컨테이너가 동시에 실행될 수 있다.
</li></ul>
<br>

<ul><li><strong>Dockerfile</strong>
<br>: 이미지를 자동으로 빌드하기 위한 명령어 모음 파일이다.
어떤 환경을 사용할지, 어떤 명령을 실행할지 등을 정의한다.
</li></ul>
<br><br>



### Docker 설치
```
# Docker 엔진(docker.io) 설치
sudo apt install docker.io -y

# 시스템 부팅 시 Docker 자동 실행 설정
sudo systemctl enable docker

# Docker 실행
sudo systemctl start docker

# Docker 상태 확인
sudo systemctl status docker

# ubuntu 계정을 Docker 그룹에 추가
sudo usermod -aG docker ubuntu

    >> 세션 종료 후 재 접속 <<

# Docker 버전 확인
docker --version

# 실행중인 컨테이너 목록
~$ docker ps 

# 전체 컨테이너 목록
~$ docker ps -a

# 실행중인 이미지 목록
~$ docker images 

# 전체 이미지 목록
~$ docker images -a
```

<br><br>


### CI/CD
<ul><li><strong>CI(지속적 통합)</strong>
<br>: 여러 개발자가 작성한 코드를 자동으로 빌드·테스트하여 통합하는 과정이다.
</li></ul>
<br>
<ul><li><strong>CD(지속적 배포)</strong>
<br>: 테스트를 통과한 애플리케이션을 자동으로 서버에 배포하는 과정이다.

```
CI/CD는 개발자가 코드를 Push하면 자동으로
빌드(Build) → 테스트(Test) → 배포(Deploy)가 진행되도록 해준다.
```
</li></ul>
<br><br>



### GitHub Secrets 설정
<ul><li>보안이 필요한 정보(IP, 계정, 비밀키 등)는 코드에 직접 쓰지 않고 GitHub Secrets에 암호화해 저장한다.
</li></ul>
<br>

<ul><li>예시구조
<br>

| 이름 | 설명 | 예시 |
|------|------|------|
| `EC2_HOST` | 배포 서버 IP | `13.125.xxx.xxx` |
| `EC2_USER` | 서버 접속 계정 | `ubuntu` |
| `EC2_KEY` | SSH 비밀키 | `-----BEGIN RSA PRIVATE KEY-----` |

</li></ul>
<br><br>


### GitHub Actions(워크플로우 자동화 도구)
```
GitHub Actions는 CI/CD를 자동화하는 GitHub 내장 도구이다.
코드가 push되면 자동으로 Docker 이미지를 빌드하고, EC2 서버에 배포한다.
```
<br><br>

### Workflow 파일 및 Dockerfile 파일

| 파일 | 설명 | 링크 |
|------|------|------|
| `ec2_aws_deploy.yml` | GitHub Actions 배포 설정 | 🔗 [보기](https://github.com/anna0121222/actions-app/blob/master/.github/workflows/ec2_aws_deploy.yml) |
| `Dockerfile` | 서버 접속 계정 | 🔗 [보기](https://github.com/anna0121222/actions-app/blob/master/Dockerfile) |

<br>
<span>
모든 민감 정보는 ${{ secrets.변수명 }} 형식으로 .yml 파일 내부에서 참조한다.
코드에 직접 키를 작성하지 않아도 GitHub Actions 실행 시 자동으로 값이 주입된다.
</span>
<br><br>

---

### CD/CI 워크플로우 단계
<img alt="CD/CI 워크플로우 단계" src="https://github.com/user-attachments/assets/132bb760-4fdd-4770-b304-a7f6bcc69a16" />
<br><br>

<p align="right"><a href="#코리아-IT-아카데미-국비과정">⬆️ 처음으로</a></p>
