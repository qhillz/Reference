#### **1) styled-components란?**

styled-components란 Javascript 파일 내에서 CSS를 사용할 수 있게 해주는 대표적인 CSS-in-JS 라이브러리로 React 프레임워크를 주요 대상으로 한 라이브러리입니다.

 

물론, 이러한 인라인 스타일링이 별로 달갑지 않은 분들도 계실 것 같습니다.

또한, 저의 경우에도, 인라인 스타일링을 선호하지 않는 편입니다.

 

그럼에도 불구하고 제가 styled-components를 사용하게 된 계기는,

우선 React의 경우 컴포넌트가 많으면 많아질수록 분리되어 있는 CSS 파일들을 일일이 찾아 수정하는 것이 얼마나 귀찮고 짜증 나는 일인지는 다들 동감하실 겁니다.

만약 styled-components를 사용하신다면, CSS를 컴포넌트화하여 JSX로 사용할 수 있습니다.

뿐만 아니라, 결정적인 요인은 바로 CSS에 Props를 사용할 수 있다는 점입니다.

React의 주요 메커니즘 중 하나인 Props를 CSS에 적용할 수 있다는 것 때문에 특정 컴포넌트에서는 styled-components를 적용하는 것이 엄청난 효율을 가져오는 것 같습니다.

 

이러한 매력을 저만 느꼈던 것이 아닌지 styled-components는 현재 npm에서 주마다 약 160만번이나 다운로드 되고 있으며 인기 있는 대세 라이브러리가 되었습니다.



#### **styled-components 설치**

간단하게 npm 혹은 Yarn을 이용하여 설치하실 수 있습니다.

 

**(1) npm 설치 명령어**

npm install styled-components

 

**(2) Yarn 설치 명령어**

yarn add styled-components

 

설치 완료 후, 적용하실 프로젝트 파일에

임포트 하여 본격적으로 사용하시면 되겠습니다!





## METHOD 2: Styling links using 'styled.componentName' format.

If you are familiar with styled components, you should know that `styled` is like the very basic thing you import from styled-components.`styled` together with 'tagNames' (e.g div or li or h1 etc) or a valid component name can be used to apply styles to a component.

The reason why we can use the latter one i.e component name, is because we have imported a component here that is `Link`, now we can pass this `Link` like this:

```
const StyledLink  = styled(Link)`
     //some CSS styles here
`;
```



**Explanation** : I know this one's a little tricky but here it goes. So basically what we are doing here is, we are creating a new component and telling it, "Hey I am a new component and I want to be like Mr.Link but in a stylish manner, so I am going to take all of the Mr.Link characteristics and add a little bit a style of my own". So in the end the code looks something like this:

```
const StyledLink = styled(Link)`
  color: Blue;
  text-decoration: none;
  margin: 1rem;
  position: relative;
`;

function Nav() {
  return (
    <NavUnlisted>
      <StyledLink to="/">Home</StyledLink>
      <StyledLink to="/about">About</StyledLink>
    </NavUnlisted>
  );
}
```



**Solution** : Now you can style your `Link` directly by creating another component instance i.e StyledLink, and then applying style to it.

**Conclusion** : This is a cleaner way than METHOD-1 because unlike in the earlier method, here we are actually writing CSS. What I meant by is that - in METHOD-1,we had to write `textDecoration` instead of `text-decoration`. Are you just noticing this now ? Greatttt !