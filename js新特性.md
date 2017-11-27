##document.elementFromPoint(x,y)
这是一个根据位置查找页面元素的方法，在写拖拽是，经常要用到的方法；

###浏览器差异以及解决办法：
While writing a new drag & drop component, i came across the javascript function elementFromPoint(x,y).
The elementFromPoint method returns the DOM node located at the coordinates x,y. This method is truly helpful when it comes to detecting a drop target. You simply get the node at the mouse position with elementFromPoint at the coordinates the drop occured and walk up through the DOM tree untill you find a valid drop target. From a jQuery point of view, this means only using $(nodeUnderPointXY).closest('myDropTargetSelector') on the node.
For more information on this elementFromPoint, see quirksmode’s compatibility table and a demo.
But unfotunately there is a big drawback !!!
I.e. there are incompatibilities between browsers in wether to use the absolute document coordinates or the relative window coordinates to detect the element.
Safari 4 and Opera 10.10 need the absolute coordinates, whereas IE and Firefox need the the relative ones. In case of a mouse event, this means the difference between pageY and clientY. clientY is the relative value which is measured from to the top left corner of the viewport. pageY is the absolute value, which is measured from the top left corner of the document. The following picture demonstrates the difference.
As you can see, there won’t be any problems if the page is not scrolled. In this case pageY and clientY are pointing to the same point of the document. But the moment the page is scrolled, both values get out of sync.
A solution to the problem
Of course we could check browsers & versions and then decide which coordinates to pass to the method. But the better way will always be feature detection. In the following i try to demonstrate a way on how to detect which coordinates are needed and then wrap these results in a new elementFromPoint method. At first we take a look at the w3c specification on the elementFromPoint method.
The w3c specification says:
The elementFromPoint(x, y) method, when invoked, must return the element at coordinates x,y in the viewport. The element to be returned is determined through hit testing. If either argument is negative, x is greater than the viewport width excluding the size of a rendered scroll bar (if any), or y is greather than the viewport height excluding the size of a rendered scroll bar (if any), the method must return null. If there is no element at the given position the method must return the rootelement, if any, or null otherwise.
Two things are important.
First: passing relative coordinates (viewport) is the default solution.
And second: if you pass coordinates which are out of the bounds of the viewport, the method must return null, whereas if the coordinates are inside the viewport’s bounds, it will at least return the root element.
This is where we start with our feature detector:
In case the document isn’t scrolled we don’t have to do any checks, as clientY and pageY will always point to the same location.
In case the page is scrolled we take the scrollamount, add it to the viewport’s height and then substract 1px. In jQuery this means $(document).scrollTop() + $(window).height() -1. This coordinate points to the bottom-most location of the viewport, if absolute coordinates are used, but exceeds the viewport, if relative coordinates are used. So if document.elementFromPoint( 0, $(document).scrollTop() + $(window).height() -1 ) returns null, the browser uses relative coordinates (clientY), and if the browser returns at least some node (possibly the root node), the browsers uses absolute coordinates (pageY).
And here are all these thoughst joined into a script:
(function ($){ var check=false, isRelative=true; $.elementFromPoint = function(x,y) { if(!document.elementFromPoint) return null; if(!check) { var sl; if((sl = $(document).scrollTop()) >0) { isRelative = (document.elementFromPoint(0, sl + $(window).height() -1) == null); } else if((sl = $(document).scrollLeft()) >0) { isRelative = (document.elementFromPoint(sl + $(window).width() -1, 0) == null); } check = (sl>0); } if(!isRelative) { x += $(document).scrollLeft(); y += $(document).scrollTop(); } return document.elementFromPoint(x,y); }})(jQuery);

##解释：
![中文解释][http://www.360doc.com/content/14/0713/12/9200790_394074586.shtml]