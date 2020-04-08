---
title: leetcode每日一题(旋转矩阵)
date: 2020-04-07 15:30:44
tags: leetcode
---

<h5>题目描述</h5>
<p>给你一幅由 N × N 矩阵表示的图像，其中每个像素的大小为 4 字节。请你设计一种算法，将图像旋转 90 度。
不占用额外内存空间能否做到？
</p>
第一种算法，引入辅助数组，再复制

```javaScript
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */

 var rotate = function (matrix) {
  const l = matrix[0].length
  const h = matrix.length
  var arr = new Array(l)
  for (let i = 0; i < l; i++) {
    arr[i] = []
  }
  for (let i = 0; i < matrix[0].length; i++) {
    for (let j = 0; j < matrix.length; j++) {
      arr[i][j] = matrix[matrix.length - 1 - j][i]
    }
  }
  for (let i = 0; i < h; i++) {
    for (let j = 0; j < l; j++) {
      matrix[i][j] = arr[i][j]
    }
  }
}
```

第二种解法，直接对原数组操作，需要观察规律

```javascript
var rotate = function (matrix) {
  const length = matrix.length

  for (let i = length - 1; i >= 0; i--) {
    for (let j = 0; j < length; j++) {
      matrix[j].push(matrix[i][j])
    }
  }

  for (let i = 0; i < length; i++) {
    matrix[i].splice(0, length)
  }
}
```
