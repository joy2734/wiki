# JavaScript(개념정리)


## ES6(ECMAScript 2015)


## Promise, Callback


## apply, call


## async, await
 
 - `async` 를 함수에 붙이면 항상 Promise를 반환한다.
```javascript
    async function f(){
        return 1; or return Promise.resolve(1);
    }
    f().then(alert) //1
```
 - `await` 는 async 함수 안에서만 동작한다.(중요!!!!)
 - promise 가 완료(resolve) 될때까지 기다린다.
 ```javascript
    async function f() {

        let promise = new Promise((resolve, reject) => {
            setTimeout(() => resolve("완료!"), 1000)
        });

        let result = await promise; // 프라미스가 이행될 때까지 기다림 (*)

        alert(result); // "완료!"
    }

 ```
 - fetch함수 자체가 Promise를 반환
 ```javascript
 async function showAvatar() {

  // JSON 읽기
  let response = await fetch('/article/promise-chaining/user.json');
  let user = await response.json();

  // github 사용자 정보 읽기
  let githubResponse = await fetch(`https://api.github.com/users/${user.name}`);
  let githubUser = await githubResponse.json();

  // 아바타 보여주기
  let img = document.createElement('img');
  img.src = githubUser.avatar_url;
  img.className = "promise-avatar-example";
  document.body.append(img);

  // 3초 대기
  await new Promise((resolve, reject) => setTimeout(resolve, 3000));

  img.remove();

  return githubUser;
}

showAvatar();
 ```

## Closure(클로저)