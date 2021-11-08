给一个正整数，把第k位扣出来，看是不是1 ， k是从右往左数的



k = 0 --> lesast significant bit

solution 1:

任何位 & 1 等于它自身
if（x & (k << 1) == 0）  ==> b3 == 0
else  ==> b3 == 1


solution 2:
(x >> k ) & 1 
solution 2的结果直接告诉我们要求的那一位是多少


bIt setter

把第k位设为1,k从右往左数:
x = x | (1 << k)



把第k位设为0：

x = x & ~(1 << k)


