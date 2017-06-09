# 多栏长度相等CSS解决方案
## 通过 background-image的方案解决

```
// html
<div id="page-wrap">        
        <div class="five-columns group">
            <div class="col"><p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.</p></div>
            <div class="col"><p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies mi vitae est. Mauris placerat eleifend leo.</p></div>
            <div class="col"><p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.</p></div>
            <div class="col"><p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies mi vitae est. Mauris placerat eleifend leo.</p></div>
            <div class="col"><p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.</p></div>
        </div>
    </div>

// css
        #page-wrap { width: 80%; margin: 60px auto; }
#page-wrap > div { margin: 0 0 50px 0; min-width: 500px; width: 100%; }

.group:after {
     visibility: hidden;
     display: block;
     font-size: 0;
     content: " ";
     clear: both;
     height: 0;
     }
.group { display: inline-block; }

.five-columns { 
    background-image: -webkit-gradient(
        linear,
        left top,
        right top,
        color-stop(0, #eee),
        color-stop(20%, #eee),
        color-stop(20%, #ccc),
        color-stop(40%, #ccc),
        color-stop(40%, #eee),
        color-stop(60%, #eee),
        color-stop(60%, #ccc),
        color-stop(80%, #ccc),
        color-stop(80%, #eee),
        color-stop(100%, #eee)
    );      
    background-image: -webkit-linear-gradient(
        left, 
        #eee, 
        #eee 20%,
        #ccc 20%,
        #ccc 40%,
        #eee 40%,
        #eee 60%,
        #ccc 60%,
        #ccc 80%,
        #eee 80%,
        #eee 100%
    );
    background-image: -moz-linear-gradient(
        left, 
        #eee, 
        #eee 20%,
        #ccc 20%,
        #ccc 40%,
        #eee 40%,
        #eee 60%,
        #ccc 60%,
        #ccc 80%,
        #eee 80%,
        #eee 100%
    );
    background-image: -ms-linear-gradient(
        left, 
        #eee, 
        #eee 20%,
        #ccc 20%,
        #ccc 40%,
        #eee 40%,
        #eee 60%,
        #ccc 60%,
        #ccc 80%,
        #eee 80%,
        #eee 100%
    );
    background-image: -o-linear-gradient(
        left, 
        #eee, 
        #eee 20%,
        #ccc 20%,
        #ccc 40%,
        #eee 40%,
        #eee 60%,
        #ccc 60%,
        #ccc 80%,
        #eee 80%,
        #eee 100%
    );
}
        .five-columns .col {
            width: 16%; float: left; padding: 2%;
        }
```

## margin-bottom padding-bottom

```
// html
<div id="page-wrap">
  <div id="one-true" class="group">
            <div class="col"><h3>I am listed first in source order.</h3><p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.</p></div>
            <div class="col"><p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies mi vitae est. Mauris placerat eleifend leo.</p></div>
            <div class="col"><p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.</p></div>
</div>
</div>
// css
#page-wrap { width: 80%; margin: 60px auto; }
#page-wrap > div { margin: 0 0 50px 0; min-width: 500px; width: 100%; }

#one-true { overflow: hidden; }
        #one-true .col {
            width: 27%;
            padding: 30px 3.15% 0; 
            float: left;
            margin-bottom: -99999px;
            padding-bottom: 99999px;
        }
        #one-true .col:nth-child(1) { margin-left: 33.3%; background: #ccc; }
        #one-true .col:nth-child(2) { margin-left: -66.3%; background: #eee; }
        #one-true .col:nth-child(3) { left: 0; background: #eee; }
        #one-true p { margin-bottom: 30px; } /* Bottom padding on the column doesn't work */
```

## flex布局

```
//html
  <div class="flexbox">
  <div class="col"><h3>I am listed first in source order.</h3><p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.</p></div>
  <div class="col"><p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante.</p>
    <p>Donec eu libero sit amet quam egestas semper. Aenean ultricies mi vitae est. Mauris placerat eleifend leo.</p>
    <p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante.</p>
    <p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.</p>
  </div>
  <div class="col"><p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.</p></div>
</div>

//css
.flexbox {      
  display: -webkit-flex;        
  display: -ms-flexbox;     
  display: flex;
  overflow: hidden;
}
.flexbox .col {
  flex: 1;
  padding: 20px;
}
.flexbox .col:nth-child(1) { 
  background: #ccc; 
  -webkit-order: 1; 
      -ms-flex-order: 1; 
          order: 1;
}
.flexbox .col:nth-child(2) { 
  background: #eee;
  -webkit-order: 0;
      -ms-flex-order: 0;
          order: 0;
}
.flexbox .col:nth-child(3) { 
  background: #eee;
  -webkit-order: 2;
      -ms-flex-order: 2;
          order: 2;
}

body {
  padding: 20px;
}
```


