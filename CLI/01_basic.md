# Basic CLI

## 폴더(directory) 관련

폴더 상징 특수기호

- `~`
  - Home Directory 의미
  - 위치는 일반적으로 /C/Users/[계정명]
- `/`
  - Root 폴더-최상단을 의미
- `.`
  - 현위치 의미
- `..`
  - 하나 위의 위치 의미

## 명령어

- `cd [대상폴더]`
  - [대상폴더] 로 이동
  - change directory 의 약자
- `ls`
  - 현재 폴더 내의 파일 목록
  - list 의 약자
- `rm`
  - 제거하기
  - remove 의 약자
    - $ re *.py → py 확장자명 file 모두 삭제
- `mkdir`
  - directory 생성
  - make directory 의 약자
- `touch`
  - 파일 생성
  - 파일명 뒤에 확장자명 기재 필수
    - $ touch CLI → CLI 파일 생성
    - $ touch CLI.txt → CLI.txt (텍스트)파일 생성

```
$ mkdir TIL
$ cd TIL
$ mkdir CLI
$ cd CLI
$ touch 01_basic.md
```

```python
def new_func(args):
	print('hi')
```

```javascript
function hello
```



## Summary

| 명령어 | 설명                | 상세                  |
| ------ | ------------------- | --------------------- |
| `ls`   | 현 폴더 목록 보여줌 | `ls -a` 전체 보여주기 |
|        |                     |                       |
|        |                     |                       |
|        |                     |                       |
|        |                     |                       |