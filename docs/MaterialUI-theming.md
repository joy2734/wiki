# MaterialUI Theming


## Spacing

 - 기본적으로 8px을 추천한다. 거기에 spacing 2 값을 줘서 8 * 2 = 16px이 적용된다.

```javascript
const theme = createMuiTheme();

theme.spacing(2) // = 8 * 2
```

 - makeStyles 사용시 theme 객체를 사용할 수 있다.
```javascript
const useStyles = makeStyles((theme) => ({
  root: {
    flexGrow: 1,
  },
  menuButton: {
    marginRight: theme.spacing(2),
  },
  title: {
    flexGrow: 1,
  },
}));
```