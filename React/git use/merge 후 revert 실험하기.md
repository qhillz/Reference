## merge 후 revert 실험하기



![image-20230610194842791](C:/Users/qhill/AppData/Roaming/Typora/typora-user-images/image-20230610194842791.png)

two 브랜치를 master에 merge 후의 결과이다. 



![image-20230610195018720](md-images/image-20230610195018720.png)

```
git revert HEAD
```

위의 코드를 통해서 master와 two가 merge 되기 전으로 되돌아갔다.



![image-20230610195202841](md-images/image-20230610195202841.png)



밑은 revert에 대해서 참고할 내용. commit2 커밋아이디를 revert 할 경우 commit2 내용이 삭제된 commit4가 자동적으로 등록되어진다. 

![image-20230610195359536](md-images/image-20230610195359536.png)

revert 자체는 Several Commit에서 특정 Commit을 제외하고 새롭게 나머지 Commit을 융합시켜주는 기능이라는걸 기억하자.



## git restore(복구) 사용방법

![image-20230610195656675](md-images/image-20230610195656675.png)

초기 "2.txt" 내용이 위와 같고


![image-20230610200048628](md-images/image-20230610200048628.png)

그리고 "2.txt"를 위와 같이 수정하고 변경시키고 싶다면.



```
git restore "2.txt"
```

해당 코드를 입력하게 되면 현재 "2.txt"가 commit 된 버전으로 백업되어진다. 



만약 전체를 복구하고 싶다면
```
git restore .
```



## git reset으로 해당 브랜치로 되돌아가기

![image-20230610200556453](md-images/image-20230610200556453.png)

만약 이렇게 여러 브랜치가 생성되었고 코드의 에러가 너무 심각하여 "first-commit"으로 되돌아가고 싶다면

```
git reset --hard e2da99e
```


이런식으로 코드를 적용해주는데 이렇게 되면 특정 commit이 제외되는 revert와는 다르게 커밋 아이디 e2da99e로 아예 회귀하게 되어버린다.



![image-20230610201126679](md-images/image-20230610201126679.png)

이런식으로 HEAD가 "first-commit" 부분으로 되돌아갔음을 알 수 있다.



## 현재 브랜치 이름을 변경하는 방법

```
git branch -M main
```



## 로컬 리포지터리를 원격 리포지터리에 옮겨보자 

![image-20230610210549285](md-images/image-20230610210549285.png)



git origin 변수를 위와 같이 "https:*//github.com/codingapple1/lesson.git*" 설정해 주겠다.

구조는 아래와 같음.



git remote add 변수명 저장소주소





설정해준다음 아래와 같이 코드를 작성하면,



```
git push -u origin main 
```

해당 -u 옵션은 입력한 주소를 기억하라는 의미.



## 원격 repo에서 로컬 repo로

```
git clone 원격저장소주소
```



## .gitignore를 사용해서 특정 파일 업로드 방지

![](md-images/image-20230610211601654.png)



현재 .gitignore 파일에는 

```
*.txt
```

와 같이 내용이 적혀져있고 "1.txt"와 "2.txt"는 이미 원격 repo에 upload되어진 상태.

"3.txt"와 "4.txt"는 아직 upload되어지지 않았고 이는 추후에 원격 repo upload시 반영되지 않는다.







