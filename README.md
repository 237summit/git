# git 소개

**git**은 컴퓨터 파일의 변경사항을 추적하고 여러 명의 사용자들 간에 해당 파일들의 작업을 조율하기 위한 **분산 버전 관리 시스템**으로 리눅스를 개발한 리누즈 토발즈가 만들었다. 
소프트웨어 개발에서 소스 코드 관리에 주로 사용되지만 어떠한 집합의 파일의 변경사항을 지속적으로 추적하기 위해 사용될 수 있다.
Git 자체는 **오픈 소스**이며 저장소는 [https://github.com/git/git](https://github.com/git/git "https://github.com/git/git")이다

##  Git 사용법 배우기
인터넷에 공개된 자료가 매우 많다.  

-   [간단히 보는 git 사용법](http://rogerdudler.github.io/git-guide/index.ko.html "http://rogerdudler.github.io/git-guide/index.ko.html")
    
-   [누구나 쉽게 이해할수 있는 Git 입문](http://backlogtool.com/git-guide/kr/intro/intro1_1.html "http://backlogtool.com/git-guide/kr/intro/intro1_1.html")
    
-   [생활코딩](https://namu.wiki/w/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9 "생활코딩")  -  [Git1](https://www.youtube.com/playlist?list=PLuHgQVnccGMCNJESahrVV-uYGMNYK_vMf "https://www.youtube.com/playlist?list=PLuHgQVnccGMCNJESahrVV-uYGMNYK_vMf"),  [Git2](https://www.youtube.com/playlist?list=PLuHgQVnccGMCNJESahrVV-uYGMNYK_vMf "https://www.youtube.com/playlist?list=PLuHgQVnccGMCNJESahrVV-uYGMNYK_vMf")
    
-   [progit](https://www.oss.kr/oss_guide/show/2c619df7-40d6-43de-af7a-2b0db6c16538) - GitHub의 CIO가 직접 쓴 책을 번역한 자료.

# git 사용하기

## 1. git install
https://git-scm.com/download
사이트에 접속하여 운영체제 버전에 맞게 설치

## 2. 구성파일 생성
구성파일 생성하기

    $ cd
    $ ls -al | grep .git
    $ git config --global user.name seongmi
    $ git config --global user.email seongmi.lee@gmail.com
    $ ls -al | grep .git
    -rw-rw-r--. 1 smlee smlee  54 Apr 18 14:26 .gitconfig

    $ cat .gitconfig
    [user]
        name = seongmi
        email = seongmi.lee@gmail.com

##  3. GIT Workflow
	WorkingDir        StagingArea       Repository
         <-------------------------------  git clone
         git add--------->|
                          |------- commit -->

## 4. Ignore : 리포지토리에서 무시할 파일 목록을 설정
  - OS가 생성하는 파일, Log 파일등은 repository에 기록되지 않도록 구성, 
  - 예를들어 이클립스의 settings 와 같은 것에는 사용자 정보가 저장될수 있다. 이런것이 commit되는 것을 예방한다.
  - ignore 할 파일 : 개발되는 프로젝트/프로그램에 따라 미리 구성해 놓는것이 좋다.

        $ mkdir gitexam; cd gitexam
	$ mkdir git_test
        $ cd git_test
        $ git init
        $ vim .gitignore
		.DS_Store
		*.log
		*.iml
		temp/

		$ touch .DS_Store
		$ echo 'Hello git!' > index.html

		$ ls -al
		total 8
		drwxrwxr-x. 2 smlee smlee  59 Apr 18 14:28 .
		drwx------. 7 smlee smlee 194 Apr 18 14:27 ..
		-rw-rw-r--. 1 smlee smlee   0 Apr 18 14:27 .DS_Store
		-rw-rw-r--. 1 smlee smlee  29 Apr 18 14:27 .gitignore
		-rw-rw-r--. 1 smlee smlee  11 Apr 18 14:28 index.html

		$ git status
		On branch master

		No commits yet

		Untracked files:
		  (use "git add <file>..." to include in what will be committed)
		        .gitignore
		        index.html

		nothing added to commit but untracked files present (use "git add" to track)

** .DS_store 파일의 목록은 표시되지 않는다. ignore됨.

## 5. git commands
- init : 현재 디렉토리를 git repository로 설정하는 명령. 
   init을 하면 해당 디렉토리에 .git이라는 파일이 생성됨. 
- status : git repository의 현재 상태 조회
- add : working dir의 파일들을 Staging Area로 추가
- commit : StagingArea의 파일들을 repository 에 추가
- log : 이전에 작성한 commit이나 파일의 변경을 추적
- diff : 이전 commit과 현재 디렉토리를 비교
- branch :  개발을 병렬적으로 진행
- tag : branch와 유사하나. branch는 파일이나 branch변경되면 마지막 변경을 추적. 
- checkout : branch를 이동하거나 특정파일을 내려받는
- merge : 병렬적으로 정의한 branch를 하나의 branch로 병합

### 1) init
init : 현재 디렉토리를 git repository로 설정하는 명령. init을 하면 해당 디렉토리에 .git이라는 파일이 생성됨. 

	$ mkdir init_test
	$ cd init_test

	$ **git init**
	Initialized empty Git repository in /home/smlee/init_test/.git/


	init 명령실행하면 .git 디렉토리와 설정 파일들이 만들어짐.
	$ ls .git/
	$ ls -l .git
	total 7
	-rw-r--r-- 1 HPE 197121 130  4월  9 08:53 config
	-rw-r--r-- 1 HPE 197121  73  4월  9 08:53 description
	-rw-r--r-- 1 HPE 197121  23  4월  9 08:53 HEAD
	drwxr-xr-x 1 HPE 197121   0  4월  9 08:53 hooks/
	drwxr-xr-x 1 HPE 197121   0  4월  9 08:53 info/
	drwxr-xr-x 1 HPE 197121   0  4월  9 08:53 objects/
	drwxr-xr-x 1 HPE 197121   0  4월  9 08:53 refs/

	$ cd .git/
	$ cat config
	[core]
	        repositoryformatversion = 0
	        filemode = false
	        bare = false
	        logallrefupdates = true
	        symlinks = false
	        ignorecase = true

	git 구성파일에 등록
	$ git config user.name eonyak
	$ git config user.email seongmi.lee@gmail.com

	$ cat config
	[core]
	        repositoryformatversion = 0
	        filemode = false
	        bare = false
	        logallrefupdates = true
	        symlinks = false
	        ignorecase = true
	[user]
	        name = eonyak
	        email = seongmi.lee@gmail.com
	$ cd ..


### 2) status
git repository의 현재 상태 출력
현재 branch, 원격 branch, 현재 추적중인 파일, 변경중인 파일 등의 목록을 표시

	$ git status
	On branch master

	No commits yet

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	        .gitignore
	        index.html

	nothing added to commit but untracked files present (use "git add" to track)

#### 현재 branch가 무엇이냐? master branch
Untracked files에 .gitignore, index.html이 생성되었고, "git add <file>..." 실행하면 commit을 위한 파일이 stagingArea로 넘어간다고 설명해주고 있다. 

		WorkingDir        StagingArea   Repository
            <-------------------------------  git clone
            git add--------->|
                              |------- commit -->


### 3) add
working dir의 파일들을 Staging Area로 추가한다.
	git add 파일명
	git add index.html
	
	현재 디렉토리 아래의 모든 추적되지 않는 파일은 모두 staging으로 전달
	$ git add .	

	interactive 방법으로 추가할 수 있다.
	$ git add -i
	

	index.html을 git add로 실행하여 StagingArea로 보낸 후 
	status를 실행하면 index.html 파일은 commit 할 준비가 되어있고 표시된다.
	$ git add index.html
	warning: LF will be replaced by CRLF in index.html.
	The file will have its original line endings in your working directory

	$ git status
	On branch master

	No commits yet

	Changes to be committed:
	  (use "git rm --cached <file>..." to unstage)
	        new file:   index.html

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	        .gitignore



	about.html을 새로 생성해서 status를 다시 한번 확인해본다. 
	이때 실행 결과를 보면 index.html은 commit할 준비가 되었고, about.html과 .gitignore 파일은 add할 준비가 되었다고 표시해줌.
	index.html은 추적된 파일, about.html은 추적되지 않는 파일.

	$ echo "<html> <h1>about</h1></html>" > about.html

	$ git status
	On branch master

	No commits yet

	Changes to be committed:
	  (use "git rm --cached <file>..." to unstage)
	        new file:   index.html

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	        .gitignore
	        about.html


	staging Area에서 다시 Working dir로 빼는 것이 git rm --cached 이다.
	$ git rm --cached index.html
	rm 'index.html'

	$ git status
	On branch master

	No commits yet

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	        .gitignore
	        about.html
	        index.html

	nothing added to commit but untracked files present (use "git add" to track)

	모든 파일을 staging Area로 올리기.
	$ git add .
	$ git status
	On branch master

	No commits yet

	Changes to be committed:
	  (use "git rm --cached <file>..." to unstage)
	        new file:   .gitignore
	        new file:   about.html
	        new file:   index.html


### 4) commit
StagingArea의 파일들을 repository 에 추가
실행시 default editor가 실행되어 message를 기록하고 저장할대 commit됨
  git commit
입력할 메시지가 적으면 command line에서 입력해서 사용
  git commit -m "커밋메시지"
이전에 commit한 파일이 수정되었을때 add하지 않고 commit하는것
  git commit -a -m "커밋메시지"	
				commit 했던 것을 다시 수정하면 workDir에 있고, add하지 않고 commit할수 있음.
	$ git config core.autocrlf false
	$ git rm --cached index.html about.html .gitignore
	$ rm about.html

	$ git status
	On branch master

	No commits yet

	Changes to be committed:
	  (use "git rm --cached <file>..." to unstage)
	        new file:   .gitignore
	        new file:   about.html
	        new file:   index.html


	$ git add index.html
	$ git status
	On branch master

	No commits yet

	Changes to be committed:
	  (use "git rm --cached <file>..." to unstage)
	        new file:   index.html

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	        .gitignore
	        about.html


	
	편집기가 실행되어 Commit Message 를 기록하고 저장.
	저장시 commit이 실행됨.
	$ git commit
	[master (root-commit) 0d5bad8] Add index.html
	 1 file changed, 1 insertion(+)  1개 파일을 commit
	 create mode 100644 index.html

	$ touch about.html

	$ git status
	On branch master
	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	        .gitignore
	        about.html

	nothing added to commit but untracked files present (use "git add" to track)

	$ git add about.html
	$ git status
	On branch master
	Changes to be committed:
	  (use "git restore --staged <file>..." to unstage)
	        new file:   about.html

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	        .gitignore

	CLI에서 about.html을 commit message 기록해서 commit
	$ git commit -m "Add about.html"
	[master def32c6] Add about.html
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 about.html


	$ touch profile.html
	$ git commit -a -m "Add profile.html"
	On branch master
	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	        .gitignore
	        profile.html

	nothing added to commit but untracked files present (use "git add" to track)
	안됨. StagingArea에 올라가지 않았음. 이것은 commit해도 올릴수 없음.


	$ vim index.html
	<html><h1>Hello git!</h1></html>

	$ git commit -a -m "Add html tag"
	[master 08dd9db] Add html tag
	 1 file changed, 1 insertion(+), 1 deletion(-)

	$ git status
	On branch master
	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	        .gitignore
	        profile.html

	nothing added to commit but untracked files present (use "git add" to track)


	새파일은 add한 후에 commit이 가능하다.
	$ git add profile.html
	$ git status
	On branch master
	Changes to be committed:
	  (use "git restore --staged <file>..." to unstage)
	        new file:   profile.html

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	        .gitignore

	$ git commit -m "Add profile.html"
	[master 1579121] Add profile.html
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 profile.html

	$ cd ..
	$ rm -rf git_test/

	log : 이전에 작성한 commit 이력을 조회하는 명령
		git log		현재 branch에 commit 이력(title, 전체내용)을 출력
		git log --oneline	현재 branch의 commit_ID와 title message만 출력
		git log --oneline --decorate -graph --all	모든 branch의 commit이력을 출력. 여러개의 branch는 그래프로 표시.
		git log -- index.html  	index.html 파일이 변경된 commit 이력만 출력

	$ mkdir git_test
	$ cd git_test
	$ git init
	$ touch index.html
	$ git add index.html
	$ git commit -m "Add index.html"
	[master (root-commit) 5b6966d] Add index.html
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 index.html

	$ touch about.html
	$ git add about.html
	$ git commit -m "Add about.html"
	[master 6d08cc8] Add about.html
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 about.html

	$ touch profile.html
	$ git add profile.html
	$ git commit -m "Add profile.html"
	[master a164de8] Add profile.html
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 profile.html

	$ echo "<html><h1>hello</h1></html>" > index.html
	$ git commit -a -m "Add html tag"
	warning: LF will be replaced by CRLF in index.html.
	The file will have its original line endings in your working directory
	[master 05badcc] Add html tag
	 1 file changed, 1 insertion(+)

### 5) log
이전에 작성한 commit 이력을 조회하는 명령
저장소에는 각 branch별로 commit 이력이 존재하는데, 그 commit 이력을 조회하는데 사용
현재 branch에 commit 이력(title, 전체내용)을 출력
	git log
현재 branch의 commit_ID와 title message만 출력		
	git log --oneline
모든 branch의 commit이력을 출력. 여러개의 branch는 그래프로 표시.
	git log --oneline --decorate -graph --all
index.html 파일이 변경된 commit 이력만 출력	
	git log -- index.html  	

	$ mkdir git_log
	$ cd git_log/
	$ git init
	Initialized empty Git repository in /home/smlee/gitexam/git_log/.git/

	$ touch index.html
	$ git add index.html
	$ git commit -m 'Add index.html'

	$ touch about.html
	$ git add about.html
	$ git commit -m 'Add about.html'

	$ touch profile.html
	$ git add profile.html
	$ git commit -m "Add profile.html"

	index.html을 수정하고 바로 commit(-a option사용)
	$ echo "<html><h1>hello</h1></html>" > index.html
	$ git commit -a -m "Add html tag"

	로그보기
	$ git log
	commit 4f34458d105fd1413bfe310c27b0792f84e94b72
	Author: seongmi <seongmi.lee@gmail.com>
	Date:   Sat Apr 18 15:24:03 2020 +0900

	    Add html tag

	commit ccdf3ddb2081706784ec7156d59670aa58958d5c
	Author: seongmi <seongmi.lee@gmail.com>
	Date:   Sat Apr 18 15:23:14 2020 +0900

	    Add profile.html

	commit 07ce3588d3f9c1ea91fff53fd31cd8a51e95d9f8
	Author: seongmi <seongmi.lee@gmail.com>
	Date:   Sat Apr 18 15:18:38 2020 +0900

	    Add about.html

	commit 0c4216b4c2d6b26e466dd6b2ad482d0f7701d0dc
	Author: seongmi <seongmi.lee@gmail.com>
	Date:   Sat Apr 18 15:17:51 2020 +0900

	    Add index.html

	about.html 내용을 수정하고, commit해본다. 이때 상세 메시지를 함께 넣어보자.
	$ echo "<html></html>" > about.html
	$ git commit about.html
	Modify about.html

	- Add html tag

	편집기 저장후 git log 를 보면 상세 메시지도 출력됨이 확인된다.
	$ git log
	commit 0a02ae015865526fe33f6f5f11a9ac525937d15e
	Author: seongmi <seongmi.lee@gmail.com>
	Date:   Sat Apr 18 15:33:18 2020 +0900

	    Modify about.html

	    - Add html tag

	commit 4f34458d105fd1413bfe310c27b0792f84e94b72
	Author: seongmi <seongmi.lee@gmail.com>
	Date:   Sat Apr 18 15:24:03 2020 +0900

	    Add html tag
	...

	--oneline 옵션은 현재 branch의 commit_ID와 title message만 출력된다.		
	$ git log --oneline
	4f34458 Add html tag
	ccdf3dd Add profile.html
	07ce358 Add about.html
	0c4216b Add index.html

	--oneline, --decorate 와 -graph, --all을 모두 사용하면 어떤 branch인지 표시된다.
	$ git log --oneline --decorate --graph --all
	* 4f34458 (HEAD, master) Add html tag
	* ccdf3dd Add profile.html
	* 07ce358 Add about.html
	* 0c4216b Add index.html

	특정 파일 index.html이 어떻게 변경되었는지 출력한다.
	$ git log -- index.html
	commit 4f34458d105fd1413bfe310c27b0792f84e94b72
	Author: seongmi <seongmi.lee@gmail.com>
	Date:   Sat Apr 18 15:24:03 2020 +0900

	    Add html tag

	commit 0c4216b4c2d6b26e466dd6b2ad482d0f7701d0dc
	Author: seongmi <seongmi.lee@gmail.com>
	Date:   Sat Apr 18 15:17:51 2020 +0900

	    Add index.html

### 6) diff
다른 커밋과 Working 디렉토리를 비교하는 명령
현재 branch의 마지막 커밋과 워킹 디렉토리의 차이점을 비교
	git diff
현재 branch나 다른 브랜치의 특정 커밋과  워킹 디렉토리의 차이점을 비교			
	git diff [Commit ID]
특정 커밋의 특정 파일이 현재 워킹 디렉토리의 그 파일이 어떻게 다른지 차이점 비교		
	git diff [Commit ID] -- [파일경로]  	

	$ echo "<html></html>" > profile.html
	$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#	modified:   profile.html
	#
	no changes added to commit (use "git add" and/or "git commit -a")

	$ git diff
	diff --git a/profile.html b/profile.html
	index e69de29..18ecdcb 100644
	--- a/profile.html
	+++ b/profile.html
	@@ -0,0 +1 @@
	+<html></html>

	$ git log --oneline 
	0a02ae0 Modify about.html
	4f34458 Add html tag
	ccdf3dd Add profile.html
	07ce358 Add about.html
	0c4216b Add index.html

	index.html을 수정하고, 0c4216b index.html과 어떻게 다른지 비교해본다.
	$ vi index.html
	<html>
	       <head></head>>
	</html>

	수정하고 특정 commit id의 시점과 현재 워킹 디렉토리가 어떻게 다른지 확인
	$ git diff 4f34458
	diff --git a/about.html b/about.html
	index e69de29..18ecdcb 100644
	--- a/about.html
	+++ b/about.html
	@@ -0,0 +1 @@
	+<html></html>
	diff --git a/index.html b/index.html
	index 18ecdcb..c7fddb3 100644
	--- a/index.html
	+++ b/index.html
	@@ -1 +1,3 @@
	-<html></html>
	+<html>
	+       <head></head>>
	+</html>
	diff --git a/profile.html b/profile.html
	index e69de29..18ecdcb 100644
	--- a/profile.html
	+++ b/profile.html
	@@ -0,0 +1 @@
	+<html></html>

	특정 파일의 특정 커밋과 현재 워킹 디렉토리와 다른점을 출력
	$ git diff 4f34458 -- index.html
	diff --git a/index.html b/index.html
	index 18ecdcb..c7fddb3 100644
	--- a/index.html
	+++ b/index.html
	@@ -1 +1,3 @@
	-<html></html>
	+<html>
	+       <head></head>>
	+</html>


### 7) branch :  개발을 병렬적으로 진행
깃에서 사용하는 브랜치를 관리하기 위한 명령
브랜치를 생성, 수정, 삭제하는 등을 하는 명령
	git  branch <브랜치명>		생성
	git branch -d <브랜치명>		삭제
	git branch -m <브랜치명>		이름변경

	$ mkdir branch_test
	$ cd branch_test
	$ git init
	$ touch index.html
	$ git add index.html
	$ git commit -m "Add index.html"

	develop 이라는 이름의 branch를 생성. commit이 없는 상태에서는 브랜치를 생성할수 없다.
	$ git branch develop
	$ git branch
	  develop
	* master    <- 현재 maser 브랜치에서 작업중

	develop 브랜치 삭제
	$ git branch -d develop 
	$ git branch
	* master

	브랜치 이름 바꾸기 
	$ git branch develop
	$ git branch
	  develop
	* master
	$ git branch -m develop test
	$ git branch
	* master
	  test



### 8) Checkout
branch를 이동하거나 특정 파일을 내려 받은 워킹 디렉토리의 소스를 특정 커밋으로 변경
특정 브랜치로 워킹 디렉토리를 변경
	git checkout <브랜치명>
특정 커밋으로 워킹 디렉토리 변경
	git checkout <Commit ID>
특정 파일을 해당 브랜치 또는 커밋 상태로 파일이 변경됨
	git checkout -- [파일경로]

	$ mkdir checkout_test
	$ cd checkout_test
	$ git init
	$ touch index.html
	$ git add index.html
	$ git commit -m 'Add index.html'

	develop, release 브랜치를 생성한다.
	$ git branch develop
	$ git branch release
	$ git branch 
	  develop
	* master
	  release

	현재 작업디렉토리를 develop 브랜치로 변경해본다. 
	$ git checkout develop 
	Switched to branch 'develop'

	develop 브랜치에서 index.html을 수정하고 commit
	$ echo "<html></html>" > index.html
	$ git add index.html
	$ git commit -m 'Add html tag'
	$ cat index.html
	<html></html>

	다시 master 브랜치로 이동해서 index.html을 보면? 아무 내용도 없다. index.html에 html 태그를 넣은것은 develop 브랜치이기 때문이다.
	$ git checkout master 
	$ cat index.html 

	$ git checkout develop 
	$ cat index.html 
	<html></html>

	$ git log --oneline --decorate --graph --all
	* f0d4ded (HEAD, develop) Add html tag
	* 82910df (release, master) Add index.html
	release,master 브랜치는 둘다 82910df를 가르키고있고, develop은 html tag가 추가된 f0d4ded를 가르킨다.

	release에서 특정 파일을 생성하고 commit했을때는?
	$ git checkout release 
	$ touch about.html
	$ ls
	about.html  index.html
	$ git status 
	# On branch release
	# Untracked files:
	#   (use "git add <file>..." to include in what will be committed)
	#
	#	about.html
	nothing added to commit but untracked files present (use "git add" to track)
	커밋되지 않았을때는 master에서도 release와 동일. commitID가 동일하니까.

	$ git checkout master 
	$ git status 
	# On branch master
	# Untracked files:
	#   (use "git add <file>..." to include in what will be committed)
	#
	#	about.html
	nothing added to commit but untracked files present (use "git add" to track)

	다시 release로 돌아가서 commit하면 새로운 commitID로 release가 변경되어 master와는 달라진다.
	$ git checkout release 
	$ git add about.html
	$ git commit -m 'Add about.html'

	master에서는 about.html이 보이지 않음.
		master(index.html)
	    +------------------+-------------------+
	    |                                 		|
	  develop(f0d4ded)             release(07f39a5) 
	 index.html 수정(태그)         about.html 생성

	$ git checkout master 
	$ ls
	index.html

	$ git log --oneline --decorate --graph --all
	* 07f39a5 (release) Add about.html
	| * f0d4ded (develop) Add html tag
	|/  
	* 82910df (HEAD, master) Add index.html

	특정 commit ID로 이동해보기
	master 브랜치에서 index.html을 수정하고 commit하면 commitID가 생성된다.
	$ git checkout master 
	$ echo "<html>
	>    <head></head>
	> </html>" > index.html
	$ git add index.html
	$ git commit -m "Add html tag"

	$ git log --oneline
	f4e59bb Add html tag
	82910df Add index.html

	index.html 수정하기전 commitID(82910df)로 이동해서 index.html을 확인하면 내용이 없다.
	$ git checkout 82910df
	$ git status
	# HEAD detached at 82910df
	nothing to commit, working directory clean
	$ cat index.html 
	$ git log --oneline
	82910df Add index.html

	다른 commitID를 조회하고 이동해보다.
	$ git log --oneline --all
	f4e59bb Add html tag
	07f39a5 Add about.html
	f0d4ded Add html tag
	82910df Add index.html

	$ git checkout f4e59bb
	$ cat index.html 
	<html>
	   <head></head>
	</html>

	$ git checkout master 
	Switched to branch 'master'
	$ git log --oneline --all --decorate --graph 
	* f4e59bb (HEAD, master) Add html tag
	| * 07f39a5 (release) Add about.html
	|/  
	| * f0d4ded (develop) Add html tag
	|/  
	* 82910df Add index.html
				  (f4e59bb Add html tag index.html)
		master(82910df  index.html)
	    +------------------+-------------------+
	    |                                 		|
	  develop(f0d4ded)             release(07f39a5) 
	 index.html 수정(태그)         about.html 생성


	특정 파일을 특정 브랜치의 특정 커밋상태로 변경해보기
	$ git log --oneline 
	f4e59bb Add html tag
	82910df Add index.html

	$ git checkout  82910df -- index.html
	$ cat index.html 
	$ git checkout  f4e59bb -- index.html
	$ cat index.html 
	<html>
	   <head></head>
	</html>

### 9) Tag
branch와 유사하나, branch는 파일이나 branch변경되면 마지막 변경을 추적. 

### 10) Merge
다른 두개의 소스를 병합하는 명령
같은 파일에 대해 서로다른 브랜치에서 동일 내용을 수정하여 충돌이 발생한 경우의 예
