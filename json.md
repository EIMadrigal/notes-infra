# JSON

JSON只有2种格式：

```json
{ "key1": val1, "key2": val2 }

[val1, val2]
```

value可以是object，array，string，number，bool，null



如果存储在文本中，JSON字符串无需被引号包裹；如果代码中声明或在前后端传递，JSON字符串需要被引号包裹。



JSON对象转JSON字符串

```javascript
const jsonObj = { name: 'John', age: 30 };
// {"name":"John","age":30}
const jsonStr = JSON.stringify(jsonObj);


const jsonObjArr = ['John', 'Peter'];
// ["John","Peter"]
const jsonStr = JSON.stringify(jsonObjArr);
```



JSON字符串转JSON对象

```javascript
let jsonStr = '{ "name": "John", "age": 30 }';
// { name: 'John', age: 30 }
let jsonObj = JSON.parse(jsonStr);


let jsonStrArr = '["John","Peter"]';
// [ 'John', 'Peter' ]
let jsonObj = JSON.parse(jsonStrArr);
```

