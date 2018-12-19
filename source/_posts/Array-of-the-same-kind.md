---
title: 统计数组中相同值的个数
date: 2018-12-19 16:24:18
tags: [js,数组，Array]
categories: "JS"
---
### 统计数组中相同值的个数

```javasrcipt
function arrCheck(arr){
  var newArr = [];
  for(var i=0;i<arr.length;i++){
	var newJson = {};
    var temp=arr[i];
    var count=0;
    for(var j=0;j<arr.length;j++){
      if(arr[j]==temp){
        count++;
        arr[j]=-1;
      }
    }
    if(temp != -1){
			newJson.name = temp;
			
			newJson.num = count;
      newArr.push(temp+":"+count)
    }
  }
  return newArr;
}
arrCheck([{"name":""},2,3,3,4]);
document.write(arrCheck([1,2,3,3,4]));  
```
将数字改为JSON可统计相同JSON值出现的次数

