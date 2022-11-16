# More Vim

## 간단한 사용법

### 커서 이동

#### 한 글자

> 사용 빈도: j, k 상 / h, l 중

- h: 좌
- j: 아래로
- k: 위로
- l: 우

#### 한 단어

> 사용 빈도: 최상

- w: 한 단어 앞으로 (커서를 단어의 맨 앞으로 옮김)
- b: 한 단어 뒤로
- e: 한 단어 앞으로 (커서를 단어의 맨 뒤로 옮김)

- W: w와 동일하지만, 무조건 빈칸 ' ' 스페이스로 구분되어 있어야만 1개의 단어입니다.
- B: 상동
- E: 상동

h, l보다는 w, b, e를 더 많이 활용하는 것이 생산성에 좋습니다.

##### w, W의 차이점

w는

``` python
print(name)
```

여기에서

``` text
print
(
name
)
```

이를 4개의 text object들을 모두 하나의 단어로 구분하지만,

W는 print(name)을 하나의 단어로 취급합니다.

#### 한 문단
vim은 사이에 빈 줄 없이 빼곡히 서로 붙어 있는 줄들을 한 문단 (a paragraph)로 취급합니다.
중괄호는 문단 간의 이동을 지원하는데, 매우 유용합니다.

#### {, } (중괄호)

> 사용 빈도: 최상

커서를 이전 혹은 다음 빈 줄로 옮겨줍니다.

``` text
(커서 위치 1)
hello world my name is Kim.
Daehyun.
(커서 위치 2)

how are you doing?
(커서 위치 3)
def helloworld():
    print('hello world')
(커서 위치 4)
```

#### line start, line end

- ^: 현재 줄의 맨 앞으로 커서를 옮깁니다. 단, 현재 줄 맨 앞의 스페이스나 탭은 스킵합니다.

> 사용 빈도: 중하

- 0: 현재 줄의 맨 앞으로 커서를 옮깁니다.

> 사용 빈도: 하

- $: 현재 줄의 맨 뒤로 커서를 옮깁니다.

> 사용 빈도: 중

#### Matching Code Block

- % : 현재 커서가 위치한 곳에서부터 가장 가까운 (, {, [ 괄호들의 위치로 커서를 옮깁니다.

한번 더 누르면 matching pair의 위치, 즉 ), }, ]가 위치한 곳으로 갑니다.

계속 누르면 이동을 반복합니다.

> 사용 빈도 중상

``` cpp
int main(){ // A
    for (int i = 0; i < 5; ++i) { // B
        printf("hello world\n");
    } // B
} // A
```

#### 원래 위치로 되돌리기

> 나 다시 돌아갈래!!!

vim의 모든 커서 위치는 vim jump list라는 곳에 기록됩니다.

- ctrl + o: 기존 커서 위치로 돌아가기 (I'm out)
- ctrl + i: 돌아가기 전 커서 위치로 되돌아가기 (I'm in)

### Code editing

지금껏 낯선 커서 움직임에 적응하느라 수고 많으셨습니다.

지금까지는 코드 내에서 커서를 움직이기만 하고 딱히 코드를 수정하지는 않았는데,

이제부터 배워볼 내용은
Vim의 꽃이라고 불릴 수 있는 코드 에디팅 기능입니다.

적응하고 익숙해지신다면 vim 없이는 코딩을 하기 불편해질 정도로 코딩이 쉽고 빠르고 재밌어질 것입니다.

#### 삭제

##### 개념

- x: 현재 커서에 위치한 글자를 삭제
- r + char: 현재 커서에 위치한 글자를 char로 변경
- c + text_object: 해당 텍스트 오브젝트를 삭제 후 insert mode로 진입
- d + text_object: 해당 텍스트 오브젝트를 삭제

##### 응용 사용법

- dw: 현재 커서로부터 한 단어를 앞으로 삭제
- db: 현재 커서로부터 한 단어를 뒤로 삭제
- diw: 현재 커서의 위치와 상관없이 한 단어를 모두 삭제 (in-delete)
- daw: 현재 커서의 위치와 상관없이 한 단어를 스페이스까지 포함해서 모두 삭제 (all-delete)
- di': ' ' 안에 들어있는 모든 글자를 다 지웁니다.
- da': ' '를 포함해서 그 안에 있는 모든 글자들을 다 지웁니다.
- di": " " 안에 들어있는 모든 글자를 다 지웁니다.
- da": " "를 포함해서 그 안에 있는 모든 글자들을 다 지웁니다.
- di): ( ) 안에 들어있는 모든 글자를 다 지웁니다.
- da): ( )를 포함해서 그 안에 있는 모든 글자들을 다 지웁니다.
- di}: Quiz?
- da}: Quiz?
- di]: Quiz?
- da]: Quiz?

- D: 현재 커서로부터 줄 맨 끝까지 삭제
- dd: 현재 커서와 상관없이 한 줄을 모두 삭제

> 사용 빈도: 최상

c도 위와 동일합니다. 단, 편집이 끝난 뒤 자동으로 insert mode에 진입합니다.

저의 추천 픽:

- daw

``` text
hello world my friend! -> hello my friend!
```

- ciw

``` text
hello world my friend! -> hello too my friend!
```

- ci)

``` text
print("hello world!") -> print(name)
```

- dd

깨알팁: 3dd라고 하면 3줄이 바로 삭제됩니다.

#### 복사, 붙여넣기

위 c, d와 동일한 방법을 사용합니다. vim의 클립보드 (레지스터라고 부릅니다)에 자동으로 복사됩니다.

- p를 통해 커서 오른쪽에 붙여넣거나,

- P를 통해 커서 왼쪽에 붙여넣을 수 있습니다.

##### 주의: vim에서 복사 붙여넣기한 내용은 vim 고유의 클립보드로 복사됩니다. 시스템 클립보드로 붙여넣으려면

``` text
"*y
혹은
"+y
```

를 써야 합니다.
마찬가지로

``` text
"*p
"+p
"*P
"+P
```

등을 통해 시스템 클립보드의 내용을 붙여넣을 수 있습니다.

#### 삽입

이제 쓸모 없는 코드들을 삭제해버렸으니, 새로운 코드를 삽입할 차례입니다.

- i: 커서의 왼쪽에서부터 insert mode에 진입 (insert)

> 사용빈도: 상

- I: 현재 줄 맨 앞에서 insert mode에 진입 (insert in front of the line)

> 사용빈도: 하

- a: 커서의 왼쪽에서부터 insert mode에 진입 (append)

> 사용빈도: 상

- A: 현재 줄 맨 뒤에서 insert mode에 진입 (append to the current line)

> 사용빈도: 중상

- o: 아래에 새로운 줄을 추가하고 insert mode에 진입 (open below)

> 사용빈도: 최상

- O: 위에 새로운 줄을 추가하고 insert mode에 진입 (open above)

> 사용빈도: 최상

#### 선택 (Visual Mode)

d + text_object 하는 건 좋으나, 가끔은 직접 영역을 설정하고 싶을 때도 있습니다.
일반적인 텍스트 에디터에서는 이걸 마우스 드래그로 하는데요, vim에서는 마우스 드래그보다 더 정교하고 편리한 선택 방법을 지원합니다.

이를 위해서는 vim에서 지원하는 4가지 모드

- Insert mode
- Normal mode
- Command mode
- Visual mode

중에서 마지막,
바로 Visual mode에서 지원하는 3가지 기능입니다.

- 커서단위 선택 (일반적인 마우스 드래그): v
- 줄단위 선택 (매우 유용, 사용빈도 최상): V
- 블록단위 선택 (가끔 유용, 사용빈도 하): ctrl+v

v를 누르면 다시 v를 누르거나 esc를 누를 때까지 visual 모드에 진입합니다.
hjkl, w, b, e등으로 여전히 커서를 움직일 수 있으며, 비쥬얼 모드에 진입한 커서의 위치부터,
움직인 이후의 커서의 위치까지 모든 text를 text_object로 취급합니다.
즉, c, d, y등의 연산을 할 수 있습니다.

#### 기타 기능

- u: 되돌리기 (undo)

> 사용빈도: 상

- Ctrl + r: 되돌리기 무효 (redo)

> 사용빈도 중상

## .vimrc

지금까지의 모든 단축키들은 다른 것으로 바꿀 수 있습니다.

지금까지의 모든 기능들은 자동화 할 수도 있습니다.

vim의 자유도는 거의 무한합니다.

### .vimrc의 위치

#### macOS

~/.vimrc

#### Windows

$HOME/_vimrc

### Neovim 사용자의 경우 init.vim을 사용하시면 됩니다

#### Windows 사용자들의 init.vim 위치

``` text
~/AppData/Local/nvim/init.vim
```

#### macOS, Linux 사용자들의 init.vim 위치

``` text
~/.config/nvim/init.vim
```

### keymapping 문법

- map: 모든 경우
- nmap: 노말모드 매핑
- imap: insert mode 매핑
- vmap: visual mode 매핑

하지만 이들은 모든 조합키를 글로벌하게 바꿔버리기 별로 잘 쓰이지 않고,우리가 99% 사용할 매핑은 non-recursive keymapping, 즉 비재귀 키매핑입니다.

``` vim
inoremap jj <esc> " insert mode에서 jj 키를 누르면 자동으로 normal mode 진입.
nnoremap jj <esc> " normal mode에서 jj 키를 누르면 모든 행위를 취소해 줌.

inoremap jk <esc> " insert mode에서 jk 키를 누르면 <esc>를 대신함. 추천합니다.
nnoremap jk <esc> " normal mode에서 jk 키를 누르면 모든 행위를 취소해 줌. 추천합니다.

inoremap ,s <esc>:w<cr> ",s를 누르면 자동으로 normal mode에 진입한 뒤 파일을 저장함. 추천
nnoremap ,s :w<cr> " normal mode에서 자동으로 파일을 저장함.
nnoremap ,q :q<cr> " ,q를 누르면 vim에서 빠져나옴.
```

> 사용 빈도: 최상

위 키매핑은 vim을 쓰는 사람은 거의 대부분 자주 쓰는 키매핑입니다. 여러분들도 각자의 init.vim 혹은 .vimrc 파일에 적어넣어 둡시다.

Default로 박아뒀으면 vim 사용자가 더 많았을텐데 아쉽습니다. 하지만 대부분의 IDE에서 vim keymapping을 지원하기 때문에 언제 어디서든 거의 대부분 사용할 수 있다는 장점이 있습니다.

#### 이를 응용해서 h,j,k,l도 wasd로 매핑해두는 사람도 있나요???

맞습니다! 실제로 그러는 사람도 많습니다.

하지만, 체감 상 hjkl이 딱히 많이 쓰이지는 않으니 굳이 추천하지는 않습니다.
더 중요한 것은 w, b, e, %, {, }, 그리고 그 외 편집 기능입니다.

그리고 유닉스 진영에 hjkl단축키를 쓰는 프로그램들이 워낙 많아서, 익숙해지면 나쁘지 않습니다.

## 수고하셨습니다

이 정도만 알아가셔서 숙지하셔도 여러분들은 vim의 중수입니다!

이 외에 소개하지 않아서 아쉬운 기능으로는

- vim surround (강추)
- vim macro (가끔 특수한 경우에 구세주)
- vim plugins

등이 있으나, 시간 관계 상 소개하지 못해 아쉽게 생각합니다.

저는 저의 역할을 했으니, 더 궁금하신 분들은 추가로 vim 강의들을 찾아보시는 것을 권고드립니다.

정말 도움이 되는 feature 들이 많습니다.
