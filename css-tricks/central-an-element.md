# Central an element

Generally speaking, we have these ways to central an element

**Option1:** With flexBox

```css
#parent {
display:flex;
align-items:center;
}

#child {
//align-self:center
}
```



**Option2:** When you know the height of the child

```css
#parent {
position:relative
}

#child {
height: 200px;
position: absolute;
top: 50%;
margin-top: -100px
}
```

**Option3:** When you don't know the width of the child

```css
#parent {
position:relative
}

#child {
position: absolute;
top: 50%;
-webkit-transform: translateY(-50%);
transform: translateY(-50%)
}
```

**Option4:** When you don't know the width of the child

```css
#parent {
position:relative
}

#child {
position: absolute;
top: 0;
bottom: 0;
margin: auto
}
```



For most of the cases, we prefer using flexbox, but sometimes when it comes to a situation you need combine `flex:1, overflow:auto.height:100%,align-items:center`,  things may not work like you thought. However, there is a problem with this method when the flex item is bigger than the flex container.

Click this link for Example [https://codepen.io/jonathanliu525/pen/yLVbMQy](https://codepen.io/jonathanliu525/pen/yLVbMQy)

When you change the size of the table, you will find out that the content in the scrollable container is cutted off.



To fix that we should use margin on flex-item to central it self

Change this part 

```css
.container {
  display: flex;
  flex: 1;
  border: 1px solid green;
  justify-content: center;
  overflow: auto;
  align-items: center;
}

.content {
  width: 400px;
  height: 400px;
  background-color: pink;
}
```

to

```css
.container {
  display: flex;
  flex: 1;
  border: 1px solid green;
  justify-content: center;
  overflow: auto;
}

.content {
  width: 400px;
  height: 400px;
  background-color: pink;
  margin:auto;
}
```



Ref

> [https://stackoverflow.com/questions/33454533/cant-scroll-to-top-of-flex-item-that-is-overflowing-container](https://stackoverflow.com/questions/33454533/cant-scroll-to-top-of-flex-item-that-is-overflowing-container)
>
> [https://moduscreate.com/blog/how-to-fix-overflow-issues-in-css-flex-layouts/](https://moduscreate.com/blog/how-to-fix-overflow-issues-in-css-flex-layouts/)
>
> [https://stackoverflow.com/questions/14962468/how-can-i-combine-flexbox-and-vertical-scroll-in-a-full-height-app](https://stackoverflow.com/questions/14962468/how-can-i-combine-flexbox-and-vertical-scroll-in-a-full-height-app)
>
> [https://stackoverflow.com/questions/32551291/in-css-flexbox-why-are-there-no-justify-items-and-justify-self-properties/33856609\#33856609](https://stackoverflow.com/questions/32551291/in-css-flexbox-why-are-there-no-justify-items-and-justify-self-properties/33856609#33856609)

