# Powershell

지금까지 Linux / macOS 환경에서 Bash, Zsh 를 이용한 터미널 사용법을 배웠습니다.

오늘은 윈도우에서 Powershell, 혹은 pwsh을 이용해 똑같은 작업을 하는 방법을 배울 겁니다.

파워쉘 나무위키:
https://namu.wiki/w/PowerShell

CMD 나무위키:
https://namu.wiki/w/%EB%AA%85%EB%A0%B9%20%ED%94%84%EB%A1%AC%ED%94%84%ED%8A%B8

CMD.exe is deprecated. 
이제 CMD는 더이상 윈도우의 default shell이 아닙니다. 

그동안 윈도우창에 Command Prompt, 혹은 한글로 명령 프롬프트를 쳐가면서 이용했던 경험이 있을 겁니다. 이제 더이상 그럴 필요가 없고 훨씬 더 편리한 powershell을 사용하는 것을 권장합니다.

ls 대신 dir을 써야했던 불편한 cmd.exe는 이제 잊고 막강한 powershell의 힘을 누리면 됩니다.

파워쉘의 장점:
1. posix 명령어 지원
2. 오픈소스, 크로스플랫폼
3. 고급 shell 기능들을 pwsh(= Powershell 6+)부터 지원, 매우 강력한 Powershell 7+ 

> 아쉽지만 디폴트로 깔려있는 powershell은 Powershell 5 버전입니다.

## Powershell 은 POSIX 명령어를 지원합니다.

POSIX란 Portable OS Interface의 약자인데 자세한 건 모르셔도 되고, 결론만 말하자면, 리눅스나 macOS에서 사용하던 명령어를 그대로 가져와 사용할 수 있다는 뜻입니다.

`ls, rm, mkdir, cd, mv, echo, cat` 등 bash, zsh에서 사용하던 대부분의 간단한 명령어들을 지원합니다. 

따라서 linux나 macOS를 사용하던 이용자들이 넘어와서 딱히 새로운 걸 많이 배울 필요가 없이 바로 적응할 수 있습니다.

그래서 기초 사용법은 모두 아실 거라 믿고,
오늘 우리가 수업 시간에 배워볼 것은 다음과 같습니다.

0. 정말 간단한 사용법 요약
1. 유저 프로필 스크립트 만들어 커스터마이징 하는 법 (파워쉘에서 .bashrc, .zshrc와 같은 역할을 하는 문서는 무엇일까?)
2. 유저 alias 만드는 법
3. 유저 function 만드는 법
4. fzf, zoxide 설치하는 법

> Quiz: 현재 내가 사용하고 있는 쉘이 Powershell인지 cmd.exe인지 구분하는 방법은?
>> ls라고 입력해본 후 결과를 보면 됩니다. Powershell 이라면 현재 폴더에 존재하는 모든 파일과 폴더 이름을 출력하겠지만, cmd.exe 이라면 'ls'가 무슨 뜻인지 모른다고 불평합니다. 

## 정말 간단한 사용법
```
ls
mkdir temp
cd temp
cd ..
echo "hello"
touch main.py
rm main.py
code main.c
cat main.c
```

### 파워쉘에서 파일 익스플로러 열기
```
ii .
```

### 파일 익스플로러에서 파워쉘 열기
마우스 오른쪽 클릭 후 "터미널에서 열기" 선택

### 파워쉘에서 XXX 명령어의 위치 확인하기 (리눅스의 which)
```
get-command -all XXX
```

```
# 예시
get-command -all python
```

이것들만 알아도 못할 것이 없습니다. 이제 alias들을 만들어서 생산성을 극대화해봅시다. `.zshrc`를 수정하는 것처럼 파워쉘에서도 프로필 스크립트를 만들 수 있습니다.  

## 유저 프로필 스크립트 만들기

먼저 파워쉘 프로필 스크립트를 만들기 전에 해야 할 일이 있습니다.
파워쉘은 윈도우에서는 기본적으로 **모든 스크립트의 실행을 막아둡니다.** 아마 프로그래밍을 할 줄 모르는 초보들이 이상한 스크립트를 실행하는 것을 원천 봉쇄하려는 것 같습니다. 번거롭지만 파워쉘을 애용하는 프로그래머라면 이 설정을 고쳐줘야 합니다.

이걸 꺼주는 방법은 매우 간단합니다. 

1. 파워쉘을 관리자 권한으로 실행한다.

![image](https://user-images.githubusercontent.com/18080546/199468004-f18b747c-b998-4d38-bd87-9efe7660ed2b.png)

관리자 권한으로 실행하는 방법은 여러가지가 있습니다.

위 사진에 보이는 것처럼 윈도우 터미널에서 ctrl을 누른 상태로 새로운 파워쉘 프로필을 클릭해도 되고,

아니면 시작 버튼을 누른 후 powershell이라 적은 다음 ctrl+shift+enter를 눌러도 관리자 권한 파워쉘이 실행됩니다. 자주 쓰는 유용한 단축키이니 외워둡시다.

2. 다음과 같이 타이핑한다.
```
Set-ExecutionPolicy RemoteSigned
```

끝입니다. 이제 관리자 권한 파워쉘을 닫고, 일반 파워쉘을 다시 실행합니다.



이제 유저 프로필 스크립트를 수정해보겠습니다.

```
echo $profile
```

위와 같이 파워쉘에 타이핑하면 유저 프로필 스크립트의 위치를 출력합니다.
저는 다음과 같이 나옵니다.

```
C:\Users\kimdh\Documents\PowerShell\Microsoft.PowerShell_profile.ps1
```

리눅스 환경의 .bashrc, .zshrc보다는 파일명이 조금 길고 복잡하죠? 하지만 걱정할 것 없습니다. 

위 파일을 수정하고 싶으면 아래와 같이 타이핑해서 vscode로 $profile을 바로 열어서 수정하면 됩니다.

```
code $profile
```

해당 파일을 처음 열어보았다면 아마 아무 내용도 적혀있지 않을 겁니다.

거기에 `echo "hello"`
라고 적어보고 파워쉘을 닫았다 다시 열어봅시다. 새로운 파워쉘이 실행될 때마다 hello 문구를 출력하는 것을 관찰할 수 있습니다.

### alias 만들기
zsh와 달리 powershell에서의 alias는 정말 단순히 명령어의 이름만 바꾸는 용도입니다. 별로 자주 쓰이지 않습니다. function을 더 많이 쓴다고 보시면 됩니다.

```
set-alias cz zi

set-alias co code
```

### function 만들기
파워쉘 프로필 스크립팅의 꽃이라고 할 수 있습니다. zsh와 똑같이, mc, cl, x 등 우리가 지금껏 만들어 온 거의 모든 편의 기능들을 똑같이 구현할 수 있습니다.

아래는 예시 프로필 스크립트입니다.

```powershell
function hw() {
  cd "$home/Documents/homework"
}


function which() {
  get-command -all @args
}


function gst() {
  git status
}


function gad() {
  git add @args
}


function profile() {
  code $profile
}


function mc() {
  try {
    mkdir @args
  }
  catch [System.IO.IOException] {
    echo "Already exists!"
  }
  
  cd @args
}


function cl {
  [CmdletBinding()]
  param(
    [Parameter(ValueFromPipeline)]
    $_cd_paths
  )
  
  if ($null -ne $_cd_paths) {
    _cd $_cd_paths
  }
  
  ls
}


function x() {
  if (test-path main.py){
    python main.py @args
  }
  elseif (test-path main.js) {
    node main.js @args
  }
  elseif (test-path ./src/main.rs) {
    cargo run
}


function cx() {
  fd -type d | fzf | cd
}


set-alias cz zi

```

## choco 설치

choco란 윈도우의 3rd-party 패키지 매니저인데, 리눅스의 apt와 같은 역할을 하는 프로그램이라고 생각하시면 됩니다.
 
fzf, fd와 같을 툴들을 깃헙에서 직접 받아서 설치해도 되지만, choco 를 이용하면 훨씬 편합니다.

명령어 한줄로 설치할 수 있고, 자동으로 $env:path에 추가해주기 때문에, 툴들을 설치한 후 환경변수를 따로 설정할 필요 없이 바로 사용할 수 있습니다.

**관리자 권한**으로 choco를 설치하세요.

https://chocolatey.org/install#individual

위 링크에서 자세한 내용을 살펴보실 수 있습니다.

```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

이걸 파워쉘에 복붙하면 설치된다고 적혀있을 겁니다. 

## fzf 설치

https://github.com/junegunn/fzf#windows

여기 들어가서 따라하면 됩니다. choco, scoop의 사용법을 모른다면 그냥 pre-built binary를 받아서 설치하면 됩니다.

하지만 choco 를 사용해 설치하면 자동으로 $env:path에 추가해주기 때문에 더 편리합니다.

```
choco install fzf
```
를 통해 **관리자 권한**으로 fzf를 설치하고

다시 일반 파워쉘을 열면 됩니다.

## zioxide 설치

https://github.com/ajeetdsouza/zoxide#installation

따라하면 됩니다.

```
curl.exe -A "MS" https://webinstall.dev/zoxide | powershell
```

위 명령어를 실행한 후, $profile에 아래와 같은 명령어를 추가해두면 됩니다.

```
# For zoxide v0.8.0+
Invoke-Expression (& {
    $hook = if ($PSVersionTable.PSVersion.Major -lt 6) { 'prompt' } else { 'pwd' }
    (zoxide init --hook $hook powershell | Out-String)
})
```

설치 후 powershell 로 적당히 아무 디렉토리들로 cd를 하면서 데이터베이스를 만든 뒤,
zi를 타이핑해보세요.

zi는 타이핑하기 불편하기 때문에

```
set-alias cz zi
```
를 통해 cz라는 alias를 추가하거나, 기타 본인 취향에 맞는 명령얼 바꿔서 사용하시는 걸 추천합니다.

## cx 함수 만들기

지금까지 cz (=zi)를 통해 이미 방문한 폴더를 손쉽게 방문해 보았습니다. (= frecency-based search)

하지만 조금만 더 욕심을 내보겠습니다.

우리의 목표는 한번도 방문한 적 없는 폴더까지 즉시 방문하는 능력을 얻는 것입니다. (= exhaustive search)

fd라는 툴만 설치하시면 가능합니다!

**관리자 권한** 파워쉘에서

```
choco install fd
```

이후

일반 파워쉘에서

```
function cx() {
  fd -type d | fzf | cd
}
```

이러면 방문하지 않은 모든 서브 디렉토리도 갈 수 있습니다.

## 결론

여러분은 windows terminal에서 powershell을 켠 뒤,

cx나 cz를 통해 통해 원하는 폴더로 cd한 뒤,

mc를 통해 새 폴더를 만들고

code .를 통해 코딩을 시작하시면 됩니다!

## 참고 자료

좀 더 이쁜 파워쉘을 원하신다면
https://ohmyposh.dev/


