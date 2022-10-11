
# 중간고사 전에 잠시 쉬어가는 코너

* 본 수업은 11월 2일에 재개됩니다.

## 아래 코드를 본인의 .zshrc에 붙여넣으세요.
```zsh
WINHOME=$(wslpath "$(wslvar USERPROFILE)")

# examples:
alias jajungjinFolder='explorer.exe $(wslpath -w "$WINHOME/Documents/jajungjin")'
alias jajungjinJokbo='explorer.exe $(wslpath -w "$WINHOME/Documents/jajungjin/jokbo.txt")'

alias dl='' # Deep Learning
alias ml='' # Machine Learning
alias el='' # Entrepreneurship and Leadership
alias cc='' # Computer Colloquium
```

1. 본인의 윈도우 컴퓨터의 Documents 폴더에 jajungjin이라는 폴더를 추가하세요.
2. jajungjin이라는 폴더에 jokbo.txt 라는 파일을 추가하세요.
3. zsh쉘에서 jajungjinFolder, jajungjinJokbo를 각각 실행시켜보세요.

![image](https://user-images.githubusercontent.com/18080546/194996168-7f468c7f-b460-4583-9f02-2ce0d66bcc10.png)

4. 폴더와 파일이 각각 열리는 것을 알 수 있습니다.

## 이제 이것을 응용하여 자기 마음대로 시험 준비 자료들을 alias로 추가해보세요!

시험공부하기 싫어서 폴더조차 열기 귀찮을 때 큰 도움이 됩니다.


> 모두 중간고사 All A+ 받으세요!!!
