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
4. fzf, zioxide 설치하는 법

> Quiz: 현재 내가 사용하고 있는 쉘이 Powershell인지 cmd.exe인지 구분하는 방법은?
>> ls라고 입력해본 후 결과를 보면 됩니다. Powershell 이라면 현재 폴더에 존재하는 모든 파일과 폴더 이름을 출력하겠지만, cmd.exe 이라면 'ls'가 무슨 뜻인지 모른다고 불평합니다. 





