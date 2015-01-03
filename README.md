vue-dnd
=======

DnD (drag and drop) plugin for Vue.js

## example
http://jsfiddle.net/lain8dono/mrnyf79e/
### js

```js
'use strict';
Vue.use(require('vue-dnd'));
new Vue({
    el: '#list',
    data: {
      listX: ['a', 'b', 'c', 'd'],
      listY: ['A', 'B', 'C', 'D'],
    },
    methods: {
      sort: function(list, id, tag, data) {
        var tmp = list[data.index];
        list.splice(data.index, 1);
        list.splice(id, 0, tmp);
      },
      move: function(from, to, id, tag, data) {
        var tmp = from[data.index];
        from.splice(data.index, 1);
        to.splice(id, 0, tmp);
      },
      remove: function(from, tag, data) {
        from.splice(data.index, 1);
      },
    },
});
```

### html
```html
<div id="list">
  <ul>
    <li v-repeat="listX"
    v-draggable="x: {index: $index, dragged: 'dragged'}"
    v-dropzone="x: sort(listX, $index, $droptag, $dropdata)">{{$value}}</li>
  </ul>
  <div>only ↓</div>
  <ul>
    <li v-repeat="listY" v-draggable="y: {index: $index, dragged: 'dragged'}" v-dropzone="
      y: sort(listY, $index, $droptag, $dropdata),
      x: move(listX, listY, $index, $droptag, $dropdata)
    ">{{$value}}</li>
  </ul>
  <hr />
  <div class="trash" v-dropzone="x: remove(listX, $droptag, $dropdata)">trash X</div>
  <div class="trash" v-dropzone="y: remove(listY, $droptag, $dropdata)">trash Y</div>
</div>
```

### css
```css
[draggable] {
    -moz-user-select: none;
    -khtml-user-select: none;
    -webkit-user-select: none;
    user-select: none;
    /* Required to make elements draggable in old WebKit */
    -khtml-user-drag: element;
    -webkit-user-drag: element;
}
ul {
    list-style: none;
    padding: 0 0 0 5px;
    margin: 0;
    background: #666;
    width: 200px;
}
li {
    box-sizing: border-box;
    border-left: 4px solid transparent;
    padding: 0 0 0 5px;
    color: white;
}
li:hover:after {
    color: #c00;
    font-size: x-small;
    content:" (drag me)";
}
li.dragged {
    opacity: 0.4;
    color: black;
}
li.x {
    border-left: 4px dotted #00c;
}
li.y {
    border-left: 4px dotted #0c0;
}
li.over-no {
    text-decoration: line-through;
}
.trash {
    width: 300px;
    height: 30px;
    background: #666;
    color: white;
}
.trash.x {
    background: #00c;
}
.trash.y {
    background: #0c0;
}
```
