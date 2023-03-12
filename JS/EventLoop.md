![image-20220326141538733](C:/Users/qhill/AppData/Roaming/Typora/typora-user-images/image-20220326141538733.png)



Settimeout is a API provided to us by a browser.



Browser can't do render when it actually has something run in the call stack.

render is given a higher priority than your callback.

16 milliseconds, it's going to queue a rend, wait till the stack is clear.

![image-20220326144524580](md-images/image-20220326144524580-16482735260451.png)



Render Queue의 task와 Callback Queue의 task는 비동기적으로 call stack에 옮겨진다.

