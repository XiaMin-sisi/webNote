# 变量

```less
//定义变量
@boxWidth:10%;
.smallBox{ 
    width: @boxWidth;//使用变量
    height: @boxWidth;//使用变量
  }

//转义字符
@min768: ~"(min-width: 768px)";
.element {
  @media @min768 {
    font-size: 1.2rem;
  }
}
```

# 混合

一个选择器，使用另一个选择器中的所有样式。

```less
//定义一个选择器
.pinkBorder{
  border: pink thin solid;
  color:red
}
//在另一个选择器中使用上面选择器中的所有样式
.smallBox{
    .pinkBorder();//混合
  }

```

# 嵌套

使用嵌套（nesting）代替层叠或与层叠结合使用的能力。

```html
<div class="box">
    <div>
        <span></span>
    </div>
</div>
```

使得样式逻辑更加清楚。

```less
.box{
    color:bule;
    
    div{
        font-size:14px;
        
        span{
        font-size:12px;
        }
    }
}
```

# 命名空间

```less
#background(){
  .red{
    background-color: #ff4000;
  }
  .green{
    background-color: green;
  }
}

.smallBox{
    #background.green();//使用命名空间
  }
```

# 映射

```less
//映射
#buttonColor(){
  primary:blue;
  danger:red;
}

.box{ 
  color:#buttonColor[primary];//映射
}
```

# 引入其他样式

你可以导入一个 `.less` 文件，此文件中的所有变量就可以全部使用了。如果导入的文件是 `.less` 扩展名，则可以将扩展名省略掉。

```less
@import "library"; // library.less
@import "typo.css";
```

# 函数

## 自定义函数



## 系统函数

