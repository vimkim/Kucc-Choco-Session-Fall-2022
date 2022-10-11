# 쉘 함수

```bash
printHello(){
    echo "hello world!"
}
```
의 형태를 띄고 있음.

- alias 보다 강력한 기능을 지원함.

- $@를 통해 인자를 받을 수 있음

```bash
printName(){
    echo "hello $@!!"
}
```

- 다른 프로그래밍 언어들과 마찬가지로 if, else, while 문 등 제어문을 사용 가능함.

# 도전과제 정답
## cl이라는 명령어를 만들어 추가하라.
```
cl(){
  cd $@; ls
}
```
## mc 라는 명령어를 만들어 .bashrc 에 추가하라.
```
mc(){
    mkdir $@; cd $@
}
```

## x 라는 명령어를 만들어 .bashrc에 추가하라.
```
x(){
  if [ -f main.py ]; then
    python3 main.py
  elif [ -f main.c ]; then
    gcc main.c && ./a.out
  # elif [ -f bin/main.ml ]; then
  #  dune exec ${PWD##*/}
  # else
  # echo "hello"
  fi
}
```

> `&&` 뒤에 있는 명령어는 앞에 명령어가 정상 동작해야만 실행한다.
> gcc main.c 가 성공적으로 컴파일에 성공해야만 새로 만들어진 ./a.out이 실행되도록 하는 명령어줄이다. 

# zsh
https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH#how-to-install-zsh-on-many-platforms

```
sudo apt install zsh
```

현재 쉘이 zsh인지 확인하는 법:
```
echo $SHELL
```

# fzf
설치하는 방법
```
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install
``` 

`sudo apt install fzf`도 되지만 가끔 버전이 너무 낮음. git이 속편함.

그 후

.zshrc에
```
[ -f ~/.fzf.zsh ] && source ~/.fzf.zsh
```
추가. 보통 자동으로 추가되어 있음.

잘 설치되어있는지 확인하기 위해 터미널에 fzf를 쳐본다.

### fzf 사용하기 이전 알아야 할 상식
- cat hello.txt 는 hello.txt 의 내용을 터미널에 출력한다.
- `XXX | YYY` 와 같이 | (파이프) 명령어를 사용하면 XXX 명령의 결과를 YYY 프로그램에 입력한다.

예시:
```
### main.py
x = input()
print("input is", x)
```
위 파일을 만들고
```
echo "abcd" | py main.py
```
라고 하면 즉시
```
input is abcd
```
가 출력된다.

## fzf 사용법
```
### temp.txt
hello
world
my name is Kim
```
위 파일을 홈디렉토리에 만들어보고
```
cat temp | fzf
```
해본다.

# zoxide
zoxide는 frecency, 즉, frequent + recent한 폴더들에 가산점을 매겨
유저가 조금의 힌트만 제공하면 즉시 해당 폴더로 이동해준다.

```
curl -sS https://raw.githubusercontent.com/ajeetdsouza/zoxide/main/install.sh | bash
```
결과를 한번 읽어보고 
`~/.local/bin`을 소싱하지 않았다 이런 말이 나오면
.zshrc 파일에
```
PATH=~/.local/bin:$PATH
```
를 추가한다.

그 이후

```
eval "$(zoxide init zsh)"
```
를 .zshrc에 맨 밑에 추가해주면 설치 완료.

## 사용법
### z
`z xxx`
를 누르면 예전에 방문한 적 있는 xxx 폴더로 가준다.

### zi
폴더 2개 이상을 cd로 방문해본 뒤 zi를 실행해보면 된다.
매우 유용한 단축키!!
