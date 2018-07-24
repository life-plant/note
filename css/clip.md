
#clip
- 一定要设定position为absolute才会起作用
- clip对input不起作用
- clip对占位不起作用
```
.hidden{
    position:absolute;
    clip: rect(1px 1px 1px 1px); /* IE6, IE7 */
    clip: rect(1px, 1px, 1px, 1px);
}
```
