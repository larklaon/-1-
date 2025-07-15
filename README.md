# Python 개발 환경 구축

## 1. 내 컴퓨터 환경

- **운영체제:** macOS

## 2. 환경 변수란?

**환경 변수(Environment Variable)**란, 운영 체제나 프로그램이 실행될 때 참고하는 **설정 값**을 저장하는 공간입니다. 예를 들어, 파이썬을 설치한 뒤 환경 변수에 경로를 등록하면, 터미널 어디서든 python이나 pip 같은 명령어를 바로 쓸 수 있습니다.

환경 변수는 프로그램의 실행 위치, 설정 정보, 시스템 전체에 적용할 값 등을 쉽게 관리하고 공유할 수 있게 도와줍니다.

## 3. Homebrew 설치

### 3-1. Homebrew가 필요한 이유

터미널에서 프로그램을 설치할 때 Homebrew가 꼭 필요한 것은 아니지만, Mac에서 가장 편리하고 일반적인 방법입니다. Homebrew를 사용하면:

- 통일된 방법으로 모든 프로그램을 설치할 수 있습니다
- 필요한 라이브러리들을 자동으로 관리해줍니다
- 업데이트와 삭제가 쉽습니다


### 3-2. Homebrew 설치 과정

```bash
# Homebrew 설치 명령어
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 패스워드 입력 후 설치 진행
# 설치 완료 후 환경 변수 설정
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

# 설치 확인
brew --version
```


## 4. Python 개발 환경 구축

### 4-1. Python 3.8 이상 설치

```bash
# Homebrew를 이용해 Python 설치
brew install python

# 설치된 Python 버전 확인
python3 --version
# 출력된 버전이 3.8 이상이면 정상입니다.
```


### 4-2. 환경 변수 등록

```bash
# 파이썬이 어디에 설치되었는지 확인
which python3
which pip3

# 환경 변수 설정 (Apple Silicon Mac용)
echo 'export PATH="/opt/homebrew/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```


### 4-3. Python 3.13의 새로운 정책과 가상 환경

#### 4-3-1. externally-managed-environment 정책

Python 3.13부터 **PEP 668** 정책이 도입되어, 시스템 Python 환경 보호를 위해 직접적인 pip 설치가 제한됩니다:

```bash
# 이런 명령어들이 오류 발생
pip3 install flask              # ❌ 오류
pip3 install --user flask       # ❌ 오류
```

**오류 메시지:**

```
error: externally-managed-environment
```


#### 4-3-2. 가상 환경이란?

**가상 환경(Virtual Environment)**은 파이썬 프로젝트별로 독립적인 패키지 환경을 만드는 기능입니다.

**비유로 설명:**

- **시스템 전체**: 공용 작업실 (모든 사람이 사용)
- **가상 환경**: 내 전용 작업실 (나만 사용하는 독립 공간)

**장점:**

- **안전성**: 시스템 Python 환경 보호
- **격리**: 프로젝트별 패키지 관리
- **호환성**: Python 3.13 정책 준수


#### 4-3-3. 가상 환경을 이용한 Flask 설치

```bash
# 1. 가상 환경 생성
python3 -m venv flask_project

# 2. 가상 환경 활성화
source flask_project/bin/activate

# 3. 가상 환경 활성화 확인 (터미널 프롬프트 앞에 (flask_project) 표시됨)

# 4. Flask 설치
pip install flask

# 5. 설치 확인
python -c "import flask; print('Flask 설치 성공!')"
```


### 4-4. vim으로 "Hello" 반환 함수 작성

```bash
# vim으로 my_solution.py 파일 생성
vim my_solution.py
```

vim에서 다음 과정으로 함수 작성:

1. **`i` 키를 눌러 편집 모드 진입**
2. **함수 코드 입력:**
```python
def hello():
    return "Hello"

# 터미널에서 실행했을 때 Hello가 출력되도록
if __name__ == "__main__":
    print(hello())
```

3. **`Esc` → `:wq` 입력하여 저장하고 나가기**

### 4-5. 터미널에서 실행 및 테스트

```bash
# 파일 내용 확인
cat my_solution.py

# 파일 직접 실행 (Hello 출력됨)
python3 my_solution.py

# 함수 단독 테스트 (import 테스트)
python3 -c "from my_solution import hello; print(hello())"
```

**import 테스트 설명:**

- `from my_solution import hello`: my_solution.py 파일에서 hello 함수를 가져오기
- 함수가 다른 곳에서 정상적으로 사용될 수 있는지 확인하는 과정
- 코드의 재사용성과 모듈화 검증


## 5. Visual Studio Code 설치 및 설정

### 5-1. Visual Studio Code 설치

```bash
# Visual Studio Code 설치
brew install --cask visual-studio-code

```


## 5-2. Material Icon Theme 확장 설치

VS Code가 실행되면:

1. 왼쪽 메뉴에서 **네모 4개가 겹친 모양(확장 탭)** 클릭
2. 검색창에 `Material Icon Theme` 입력
3. 나오는 확장 프로그램을 **Install** 버튼으로 설치

## 제출 파일

- `my_solution.py` : hello 함수가 들어있는 파이썬 파일 
- `python_webframework.md` : 웹 프레임워크 설명 파일 
