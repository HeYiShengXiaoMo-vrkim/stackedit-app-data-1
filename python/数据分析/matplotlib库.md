### 第一个折线统计图

 1. 先声明好x,y数据
 2. 导入到plt.plot(x,y)
 3. 使用plt.show()显示

### 设置图片大小

 1. plt.figure(figsize=(长,宽),dpi=数字)dpi控制图片清晰度
 2. plt.savefig("./名称.svg") 保存图片，svg放大无锯齿，也可以是png

### 都做了什么

 1. 使用plt.plot制作折线图
 2. plt.figure设置图片大小和分辨率
 3. plt.savefig保存图片
 4. xticks设置xy轴上刻度和字符串
 5. xticks解决刻度稀疏问题
 6. 设置了标题，xy轴的lable(title, xlable, ylable)
 7. 设置字体(font, manager, fontProperties, matplotlib, rc)
 8. 绘制多个折线，多plt.plot几次
 9. 添加图例 plt.legend(),图例来源于plt.plot()时label参数的值
 10. plt.scatter(x, y) 绘制散点图
 11. plt.grid()绘制网格线
 12. plt.show()展示图片
 13. plt.hit()绘制直方图
 14. plt.bar()绘制竖着的条形图，plt.barh()绘制横着的条形图


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ2MDY2NDcyMV19
-->