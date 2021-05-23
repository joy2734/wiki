# 일렉트론

## 초기세팅
 - main": "src/index.js",//보통 일렉트론 메인process 소스명은 main.js
 - dependencies 
    "electron": "6.0.0",
    "electron-builder": "21.2.0",
    "eslint": "6.1.0",
    "eslint-config-prettier": "6.0.0",
    "eslint-plugin-prettier": "3.1.0",
    "prettier": "1.18.2"
    "electron-util": "0.12.1"
  }
 - script
    "start": "electron src/index.js",
    "final": "electron final/index.js",
    "pack": "electron-builder --dir",
    "dist": "electron-builder"

## 일렉트론 API

 - 해당 api 사용시 웹에서는 구현할 수 없는 부분이 구현가능하다.
   - 알림
   - 기본파일 드래그 앤드롭
   - 맥OS 다크모드
   - 맞춤형 메뉴
   - 강력한 키보드단축키
   - 시스템 대화상자
   - 애플리케이션 트레이-하단 앱작은아이콘?
   - 시스템정보

## 설정
 
 - 소스참고. 

## 일렉트론 배포

 - 일렉트론 빌더 vs 포지
   - 일렉트론 빌더 - 독립적인 빌드도구

 - 설정
   - appId -  app 고유식별자
             - mac - CFBundle Identifier
             - win - AppUser ModeId
             - 역방향 DNS 형식
               - ex)도메인 jseverywhere.io 인회사에 [app명] -> io.jseverywhere.[app명]
   - productName
     - 제품명?

## App 구조

 - 구성
   - 크로미넘 - 웹컨텐츠를 보여준다.
   - Nodejs - 시스템동직/내부파일시스템 동작
   - custom Api - 자주쓰이는 네이티브 func

## 메인/ Renderer 과정
 - Eletron 2가지 타입
   - Main
     - 메인은 `BrowserWindow` 인스턴스들로부터 만들어지는 웹페이지를 만들어준다. 각 `BrowserWindow` 인스턴스는 Renderer 프로세스안에 웹페이지를 동작시킨다. `BrowserWindow`가 destroy될때 각 `BrowserWindow`에 대응하는 Renderer 프로세스도 종료된다.
     - 메인은 모든 웹페이지들을 관리한다.
   - Renderer
     - Renderer는 다른 Renderer process에 영향을주지않음
     - Renderer process는 웹페이지에 GUI 동작을 수행하기위해서 `IPC`를 통해서 메인프로세스와 같이 통신한다. Renderer로부터 직접 GUI 관련 api호출은 보안관신사나/리소스 누수 때문에 제한하고있다.
 ※ 프로세스간의 통신은 IPC(inter-Process Communication) 모듈이용한다.
  - `ipMain`/`ipcRenderer`

## API

 - Electron API : Main/Renderer 에서 사용되는 모듈들..
   - election API 접근
   - 창을 생성하기 위해 메인에서 이용되는 `BrowserWindow` 클래스 호출 
```javascript
    const {app, BrowserWindow} = require('electron');
    const win = new BrowserWindow();
```
   - Renderer로부터 메인프로세스 호출하기위해서는 IPC 모듈사용
```javascript
    //메인프로세스영역
    const { ipcMain } = require('electron');
    
    //이벤트
    ipcMain.handle('perform-action',(evtent, args)=>{
        // ...do actions on behalf of the Renderer
    });

    // Renderer 프로세스 
    const { ipcRenderer } = require('electron');

    ipcRenderer.invoke('perform-action', ...args);

```

 ※ 메인 프로세스에서 오는 요청들을 검증하기위해서 중요한 api이다.

## Node.js API

  - Renderer로부터 nodejs api에 접근하기 위해서는 main.js에 `nodeIntegration` 설정 `true` 와 `contextIsolation` `false` 로 설정하여야 한다.
  - remote content를 로드하기위해서 Renderer에 nodejs api에 접근은 보안상 이유로 추천하지않음.
  - 일렉트론은 모든 nodejs api 에 접근가능

```javascript
const fs = require('fs')

const root = fs.readdirSync('/')

console.log(root)

```

## Notification

 - 3가지 os는 유저에게 `notification`을 app에 보내주는 기능을 제공.
 - `notification`을 보여주는 기술은 Main/Renderer에 따라 차이가있다.
   - Renderer - `HTML5 Notification API` 사용하여 noti 처리
   - Main - `Notification` 사용하여 noti 처리
 
 - Main noti
   - 해당 예제 메인 실행시 메인창을열고 noti정보를보여준다.
```javascript
function showNotification () {
    const notification = {
      title: 'Basic Notification',
      body: 'Notification from the Main process'
    }
    new Notification(notification).show()
  }
  
app.whenReady().then(createWindow).then(showNotification)
```

 - Renderer에 noti
   - 로드되는 페이지에 해당js 추가시 페이지 랜더시 해당 noti가 발생함.
```javascript
const myNotification = new Notification('Title', {
    body: 'Notification from the Renderer process'
  })
  
myNotification.onclick = () => {
console.log('Notification clicked')
}

```
 - os에 따라서 미묘하게 사용 차이가 있음

 - 고급알림
   - electron-windows-notifications - 스터디필요
     - ToastNotification
     - TileNotification
   - 알림 보낼수 있는지 여부감지 userland모듈 `electron-notification-state` 사용

## Recent Documents
  
 - 최근 문서 목록 보여주는곳에 보여짐.
```javascript
const { app } = require('electron')

//최근문서 목록 추가
app.addRecentDocument('/Users/USERNAME/Desktop/work.type')

//최근문서 목록 clear
app.clearRecentDocuments()
```

## Custom Dock Menu
 
  - 아이콘 context메뉴에 추가되는거같은데 production버전에서봐야할듯 

```javascript
const {Menu} = require('electron');
const dockMenu = Menu.buildFromTemplate([
  {
    label: 'New Window',
    click () { console.log('New Window') }
  }, {
    label: 'New Window with Settings',
    submenu: [
      { label: 'Basic' },
      { label: 'Pro' }
    ]
  },
  { label: 'New Command...' }
])

app.whenReady().then(() => {
  if (process.platform === 'darwin') {
    app.dock.setMenu(dockMenu)
  }
}).then(createWindow)
```

## Window TaskBar

```javascript
const { app } = require('electron')

//set tasks
app.setUserTasks([
  {
    program: process.execPath,
    arguments: '--new-window',
    iconPath: process.execPath,
    iconIndex: 0,
    title: 'New Window',
    description: 'Create a new window'
  }
])

//clear tasks
app.setUserTasks([]);
```

## Online/Offline Event Detection

 - 온/오프라인 체크
 - 런처 실행시 online은되는 offline은 어떻게 체크되는지 파악필요

## Native File Drag & Drop

 - 