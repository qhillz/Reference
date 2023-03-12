# value vs textContent

The properties "value" and "textContent" represent different things. Any *node* has a "textContent", including text nodes which are not elements. It represents the text content of the node itself along with any and all descendants.

But only input elements have a "value". It represent the input data supplied by the user or provided initially by the code. Also, input elements may have a "textContent" property but it will always be empty since they are *void elements*.



textContent는 지정된 elem의 textnode 값을 보여주는 것이다. 반면에 value와 같은 경우는 특정 elem의 입력값을 보여준다고 생각하면 된다.