## CORS PROBLEM SOLUTION

![cors1](./img/图45.png)
```js
const cors = (req,res,next) => {
  res.setHeader('Access-Control-Allow-Origin','*');
  next();
}

app.use(cors);
```
![cors2](./img/图46.png)
```js
const cors = (req,res,next) => {
  res.setHeader('Access-Control-Allow-Origin','*');
  res.setHeader('Access-Control-Allow-Headers','content-type');
  next();
}
app.use(cors);
```
![cors3](./img/图47.png)
```js
const cors = (req,res,next) => {
  res.setHeader('Access-Control-Allow-Origin','*');
  res.setHeader('Access-Control-Allow-Headers','content-type');
  res.setHeader('Access-Control-Allow-Methods','*');
  next();
}
app.use(cors);
```
