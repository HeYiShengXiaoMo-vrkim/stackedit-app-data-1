### 第k个数(快排/快选)
1. 找到分界点x, q[L], q[(L+R)/2], q[R]
2. 左边所有的数left <= x, 右边所有的数 Right >= x
3. 递归排序left, 递归排序right（快排到此）
4. 将第k个数当做分界点x，统计左元素个数`S_l`,右元素个数`S_r`
5. 如果`k<=S_l`递归左侧， 如果`k>=S_r`递归右侧，


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUzMDk2NTkxXX0=
-->