#jQuery

##jquery $(e).index()用法；
$(elem).index() // 匹配的第一个元素相对于其同胞元素(包括不同的元素的)的位置,
$(elem).index(target) 
// target相对于$(e)匹配的第一个元素的位置（$(e)匹配元素的顺序是从文档根到叶、再文档上到下）。

##eq()方法
$(elem).eq(i);查找第i个元素，负数则找最后一个元素。

##unbind()方法
$(elem).unbind()方法可以解绑由jquery绑定的一切事件。也可以解绑特定函数的事件，只要传入该函数的名称就可以解绑

