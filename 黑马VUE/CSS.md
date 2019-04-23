##### flex布局

```css
display: flex;
flex-wrap: wrap;
justify-content: space-between;
```

##### box-shadow

```css
box-shadow: 0 0 8px #ccc;
```

##### flex-direction

```css
display: flex;
flex-direction: column;
justify-content: space-between;
```

##### mt-button 并排，br 换行不生效

display: flex; 会导致这种问题。   改成 display: block;  即可解决。

##### align-items: center;

设置给父元素，子元素垂直居中。

```css
.parent: {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
```

##### vertical-align: center; 

把此元素放置在父元素的中部。