# MaterialUI (v4.11)

## Install

 - Core
<br>

 `yarn add @material-ui/core`

 - Font Icons
<br>
```html
    <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons" />
```


 - Icons
<br>

 `yarn add @material-ui/icons`

<br>
<br>

## Usage

 - '@material-ui/core/{컴포넌트명}' 임포트 후 사용. 
```javascript
import Button from '@material-ui/core/Button';
```

<br>

## Responsive meta Tag

Material UI는 모바일환경에서 우선적으로 개발되었기 때문에 헤더안에 responsive viewport meta tag 를 추가해야한다.

```javascript
<meta
  name="viewport"
  content="minimum-scale=1, initial-scale=1, width=device-width"
/>
```
<br>
<br>

## `withStyles` 사용
 - styles 객체를 만든후 with 스타일로 해당스타일속성을 적용 **this,props.classes**로 사용한다.

```javascript
import React, { Component } from 'react';
import Button from '@material-ui/core/Button'
import { withStyles } from '@material-ui/core/styles';
const styles  = {
  root: {
    background: 'linear-gradient(45deg, #FE6B8B 30%, #FF8E53 90%)',
    border: 0,
    borderRadius: 3,
    boxShadow: '0 3px 5px 2px rgba(255, 105, 135, .3)',
    color: 'white',
    height: 48,
    padding: '0 30px',
    margin : '10px'
  },
};
class StyleTutorial1 extends Component {
  render() {
    const {classes} = this.props;
    return (
      <div>
        <Button className={classes.root}>Button with Style</Button>
        <Button className={this.props.classes.root}>Button with Style</Button>
      </div>
    );
  }
}
export default  withStyles(styles)(StyleTutorial1);
```

## `makeStyles` 사용

 - @material-ui/core/styles에 makeStyles, createStyles 사용하여 스타일을 정의하고 컴포넌트 안에서 해당설정을 적용시켜사용한다. Material UI는 직관적으로 사용자 정의 스타일을 적용할 수 있도록 makeStyles React hook을 제공한다.

```javascript
import { makeStyles, createStyles } from '@material-ui/core/styles';

const useStyles = makeStyles((theme: Theme) => createStyles({
  root: {
    backgroundColor: theme.color.red,
  },
}));

export default function MyComponent {
  const classes = useStyles();
  return <div className={classes.root} />;
}
```
<br>

## CssBaseline
<br>
 - CssBaseline은 어떤 브라우저에서 돌아가느냐 상관없이 일괄적으로 스타일이 적용되게 해주는 컴포넌트이다. 해당 컴포넌트는 css를 전역에서 정규화시켜주는 것이 권장된다. 우선 최상단에 CssBaseLine 컴포넌트를 React App 최상위 컴포넌트에 추가해줘야한다.

```javascript
import React from "react"
import CssBaseline from "@material-ui/core/CssBaseline"

export default function App() {
  return (
    <>
      <CssBaseline />
      {/* 다른 컴포넌트 */}
    </>
  )
}
```
<br>

## AppBar

 - 현재 스크린과 관계된 행동/정보들을 보여준다.(상단정보 바)

<br>

## Fade

 - 화면 전이(나타나고/사라지고)가 쉽게 동작하도록 만들어주는 컴포넌트
 - in 속성 true시 감춰진다.
 - timeout 속성 사용시 사라지는 시간을 조절할 수 있다.  
    `{ enter: duration.enteringScreen, exit: duration.leavingScreen,}`

```javascript
export default Main() {
  return (
    <Fade in={check}>
      <MyComponent />
    </Fade>
  );
}
```

## InputBase

 - 

## IconButton

 - color: 컴포넌트의 테마 컬러. (default| inherit| primary| secondary)
 - disabled: true시 버튼사용이 불가능하다.
 - edge : 테두리 크기와 모양을 손상시키지않고 아이콘 왼쪽/오른쪽을 콘텐츠 위/아래에 정렬하는데 도움을준다.

```html
 <IconButton edge="end" className={classes.menuButton} color="inherit" aria-label="menu">
    <MenuIcon />
 </IconButton>
```

## Material Icons

 - 아이콘들을 해당 [https://material-ui.com/components/material-icons/](https://material-ui.com/components/material-icons/)에서 아이콘을 import 하여 사용할 수 있다.
