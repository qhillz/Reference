# React Router Dom

Switch => 둘러쌓인 route 컴포넌트중 1개만의 렌더링을 허락한다.
/ 가 있고 밑에 /topics가 있을경우에서 메인 홈페이지(/)로 이동시 밑의 route component /topics는 선택되지 않는다.

<a href="" 같은 경우는 전체페이지를 Reload하기 때문에 병목현상을 유발시킨다. 고로, 클릭된 링크의 route 컴포넌트만 바꿔주게 되는 <Link to="" 를 사용하라.

<NavLink to="" 현재 클릭된 child 요소에 'active'라는 클래스를 지정해준다.

(exact 필요.)



#### params

그러면, 먼저 params 부터 사용을 해봅시다.

App 컴포넌트에서 다음과 같이 `/about/:name` 라우트를 추가하세요.

#### `src/shared/App.js`

```javascript
import React, { Component } from 'react';
import { Route } from 'react-router-dom';
import { Home, About } from 'pages';

class App extends Component {
    render() {
        return (
            <div>
                <Route exact path="/" component={Home}/>
                <Route path="/about" component={About}/>
                <Route path="/about/:name" component={About}/>
            </div>
        );
    }
}

export default App;
```

URL 의 params 를 설정 할 때에는 `:foo` 의 형식으로 설정합니다. 이렇게 하면 foo 라는 params 가 생기는것이지요.



```react
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import * as serviceWorker from './serviceWorker';
import {BrowserRouter, Route, Switch, Link, NavLink, useParams} from 'react-router-dom';

function Home(){
    return (
        <div>
            <h2>Home</h2>
            Home...
        </div>
    )
}

var contents = [
    {id:1, title:'HTML', description:'HTML is ...'},
    {id:2, title:'JS', description:'JS is ...'},
    {id:3, title:'React', description:'React is ...'},
]

function Topic(){
    var params = useParams();
    var topic_id = params.topic_id;
    var selected_topic = {
        title:'Sorry',
        description:'Not Found'    
    }
    for(var i=0; i<contents.length; i++){
        if(contents[i].id === Number(topic_id)){
            selected_topic = contents[i];
            break;
        }
    }
    return (
        <div>
            <h3>{selected_topic.title}</h3>
            {selected_topic.description}
        </div>
    );
}

function Topics(){
    var lis = [];
    for(var i=0; i<contents.length; i++){
        lis.push(<li key={contents[i].id}><NavLink to={'/topics/'+contents[i].id}>{contents[i].title}</NavLink></li>)
    }
    return (
        <div>
            <h2>Topics</h2>
            <ul>
                {lis}
            </ul>
            <Route path="/topics/:topic_id">
                <Topic></Topic>
            </Route>
        </div>
    )
}

function Contact(){
    return (
        <div>
            <h2>Contact</h2>
            Contact...
        </div>
    )
}

function App(){
    return (
        <div>
            <h1>React Router DOM example</h1>
            <ul>
                <li><NavLink exact to="/">Home</NavLink></li>
                <li><NavLink to="/topics">Topics</NavLink></li>
                <li><NavLink to="/contact">Contact</NavLink></li>
            </ul>
            <Switch>
                <Route exact path="/"><Home></Home></Route>
                <Route path="/topics"><Topics></Topics></Route>
                <Route path="/contact"><Contact></Contact></Route>
                <Route path="/">Not found</Route>
            </Switch>
        </div>
    )
}

ReactDOM.render(<BrowserRouter><App /></BrowserRouter>, document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```



**Switch ==> deprecated되어 Routes로 대체됨.**

**여기서 Route안은 element안에 component가 묶이는 것으로 대체됨.**

```react
 <Routes>
    <Route exact path='/' element={<Home />}></Route>
    <Route path='/music' element={<Music />}></Route>
 </Routes>
```







