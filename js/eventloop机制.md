
##事件循环机制
 - js是单线程的
 - 同步任务放在主线程中执行，任务队列用来挂载异步任务（只要异步任务有了结果就放在任务队列中），当主线程中的同步任务完成后，扫描任务队列并执行任务队列中的任务；
   关键字：主线程，任务队列
 - 事件和回调函数：点击后触发事件，将回调函数也放入任务队列中。
 - event loop（事件循环机制）：主线程从任务队列中读取事件，这个过程是循环不断的，所以整个的这种机制称为event loop;
 - setTimeout也是一样的，延迟时间到了之后，将回调任务加入任务队列中；
 - 为了利用多核CPU的计算能力，HTML5提出WebWorker标准，允许JavaScript脚本创建多个线程，但是子线程完全受主线程控制，且不得操作DOM。
 - 任务会分为macrotask,microtask;setTimeout属于macrotask,而promise本身属于同步事件，then产生的异步事件属于microtask;


##总结
    事件循环机制中，事件的任务队列会分为两种：macrotask和microtask。setTimeout属于macrotask,而promise的then产生的异步事件属于microtask，当microtask有任务时会先把microtask里面的所有队列执行完再执行macrotask的任务，也就是说microtask的优先级高于macrotask。