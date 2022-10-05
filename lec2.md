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

# zsh
https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH#how-to-install-zsh-on-many-platforms

```
sudo apt install zsh
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

## 사용법
터미널에 fzf를 쳐본다.

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
