# await fetch 예시

```javascript
		async function execution() {
            let users = await getUsers(["C17AN", "Violet-Bora-Lee", "이런사용자는없습니다"]);
            console.log(users[0]);
            if(users[0].login == "C17AN"){
                alert('complete');
            }
        }

        async function getUsers(names) {
            let jobs = [];

            for (let name of names) {
                let job = fetch(`https://api.github.com/users/${name}`).then(
                    successResponse => {
                        if (successResponse.status != 200) {
                            return null;
                        } else {
                            return successResponse.json();
                        }
                    },
                    failResponse => {
                        return null;
                    }
                );
                jobs.push(job);
            }

            let results = await Promise.all(jobs);

            return results;
        }

        execution();
```



가장 주목해야할 부분은 let results = await promise.all(jobs); 부분이다. async fuction이 return을 할려 했지만 await의 메소드를 통한 call stack에 function이 microtask (promise) > resolved될때까지 기다리게 된다.