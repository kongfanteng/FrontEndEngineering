# call+apply_new_bind 原理
## call和apply原理
1. 可以改变我们当前函数的this指向
2. 还会让当前函数执行
3. 如果多个call会让call方法执行，并且把call中的this改变成fn2
```
Function.prototype.call = function(context){
  context = context ? Object(context) : window;
  context.fn = this;
  let args = [];
  for(let i = 1; i< arguments.length;i++){
    args.push('arguments['+ i +']');
  }
  let r = eval('context.fn('+ args +')');
  delete context.fn;
  return r;
}
Function.prototype.apply = function(context,args){
  context = context ? Object(context) : window;
  context.fn = this;
  if(!args){
    return context.fn();
  }
  let r = eval('context.fn('+ args +')');
  delete context.fn;
  return r;
}
function fn1(){
  console.log(this,arguments);
}
function fn2(){
  console.log(this,2);
}
fn1.call('hello');
fn1.call.call.call(fn2);
fn1.apply('hello',[1,2,3,4])
```
## new原理
### new 使用
```
function Animal(type){
  this.type = type; // 实例上的属性
}
Animal.prototype.say = function(){
  console.log('say');
}
let animal = new Animal('哺乳类');
console.log(animal.type); //哺乳类
animal.say(); // say
```
### mockNew实现new方法
```
function Animal(type){
  this.type = type; // 实例上的属性
  // 如果当前构造函数返回的是一个引用类型 需要把这个对象放回函数
  return {name: 'jw'}
}
Animal.prototype.say = function(){
  console.log('say');
}
function mockNew(){
  // Constructor => animal 剩余的arguments就是其他的参数
  let Constructor = [].shift.call(arguments);
  let obj = {}; //返回的结果
  obj.__proto__ = Constructor.prototype;
  let r = Constructor.apply(obj,arguments);
  return r instanceof Object ? r : obj;
}
let animal = mockNew(Animal,'哺乳类');
console.log(animal); // {name: "jw"}
```
## bind原理
1. bind方法可以绑定this指向
2. bind方法返回一个绑定后的函数（高阶函数）
3. 如果绑定的函数被new了 当前函数的this就是当前的实例
4. new出来的结果可以找原有类的原型
### bind使用
```
let obj = {
  name: 'jw'
}
function fn(){
  console.log(this.name);
}
let bindFn = fn.bind(obj);
bindFn();
```
### bind原理
```
let obj = {
  name: 'jw'
}
function fn(name,age){
  console.log(this.name+'养了一只'+name+age+'岁了');
}
Function.prototype.bind = function(context){
  let that = this;
  let bindArgs = Array.prototype.slice.call(arguments,1); // ['猫']
  function Fn(){}// Object.create原理
  function fBound(){
    let args = Array.prototype.slice.call(arguments);
    return that.apply(this instanceof fBound ? this : context,bindArgs.concat(args));
  }
  // 两个原型类的函数没有共用
  Fn.prototype = this.prototype;
  fBound.prototype = new Fn();
  // fBound.prototype = this.prototype;
  return fBound;
}
fn.prototype.flag = '哺乳类';
let bindFn = fn.bind(obj,'猫');
let instance = new bindFn(9);
console.log(instance.flag);
```