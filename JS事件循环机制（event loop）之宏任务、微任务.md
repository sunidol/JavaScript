## JS事件循环机制（event loop）之宏任务、微任务
结合谷歌大神的文章《Tasks, microtasks, queues and schedules》以及网络资料

首先看一段代码：

(```)

console.log('script start');

setTimeout(function() {
  console.log('setTimeout');
}, 0);

Promise.resolve().then(function() {
  console.log('promise1');
}).then(function() {
  console.log('promise2');
});

console.log('script end');

(```)

打印顺序是什么？
正确答案是
**script start, script end, promise1, promise2, setTimeout**
但是在不同浏览器上的结果却是让人懵逼的。
