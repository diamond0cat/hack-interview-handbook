![20210811053625](https://i.loli.net/2021/08/11/V2drWebp79JEiBU.png)


求多少对圆是overlapped的

方法1： brute force
两两配对，求这对是否overlapped==> 圆心距离 <= 两圆半径之和

圆心1+ 半径1   <  圆心2-半径2  ==> 没有overlap，反之有overlap

时间复杂度： o(n^2)


方法2： 
转化为interval问题， 每个圆可以转化为一个interval,我们其实只关心在横轴上的Interval

![20210811053751](https://i.loli.net/2021/08/11/aKqIPEhOMocNf17.png)


做一个转化：
circle‌ ‌-->‌ ‌‌interval‌ ‌[center‌ ‌-‌ ‌radius,‌  ‌center‌ ‌+‌ ‌radius]‌ ‌
==>‌ ‌Given‌ ‌a‌ ‌list‌ ‌of‌ ‌intervals,‌ ‌how‌ ‌many‌ ‌pairs‌ ‌of‌ ‌intervals‌ ‌are‌ ‌overlapped?‌


![20210811054234](https://i.loli.net/2021/08/11/a9byUrYmOCeiSZJ.png)

以每一个end为基准，去算overlap

