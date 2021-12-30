1. 常见node面试题自测
  https://chowdera.com/2021/07/20210717170503927m.html

2. node时间循环

理解event loop最直接的意义就是可以理清setTimout setImmediate setInterval Promise process.nextTick之间的执行顺序

event loop的每一次循环都需要依次经过上述的阶段。  每个阶段都有自己的callback队列，每当进入某个阶段，都会从所属的队列中取出callback来执行，当队列为空或者被执行callback的数量达到系统的最大数量时，进入下一阶段。这六个阶段都执行完毕称为一轮循环

https://cnodejs.org/topic/5a9108d78d6e16e56bb80882
http://www.ruanyifeng.com/blog/2018/02/node-event-loop.html