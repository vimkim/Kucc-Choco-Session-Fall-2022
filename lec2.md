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
curl -sS https://raw.githubusercontent.com/ajeetdsouza/zoxide/main/install.sh | bash