


```java
    public String longestPalindrome(String s) {
        // 构造辅助字符数组
        char[] manacher = new int[s.length() *2];
        for (int i = 0; i <s.length(); i++) {  //两端插#，每个字符中间插入#
            manacher[2 *i] = '#';
            manacher[2 *i + 1] = s.charAt(i);
        }
        manacher[manacher.length - 1] = '#';
        
        // 求辅助字符串中的最长回文半径
        //回文半径数组
        int[] pArr = new int[manacher.length]; // 记录每个字符搜索能达到的最长回文半径
        int maxLength = 0;  //记录搜索过程中最长回文子长度(保留辅助字符影响)
        
        int C = -1;  //初始中心
        int R = -1;  // 初始右边界, R代表最有的扩成功的位置
        
        for (int i = 0; i < manacher.length; i++) {
            if (i < R){  //(i在R外,暴力扩)， R变大
                
            } else {  // i在R内
                if () {  //i对称点i`的回文区域彻底在L...R内部
                    //pArr[i] = pArr[i的对称点]
                    
                } else if (){    //i对称点i`的回文区域在L...R外部
                    //pArr[i] = i...R （i到R的距离）
                } else {   //i对称点的回文区域做边界和L压线
                    //从R外开始扩， R变大 
                }
            }
        }
        
        
       // return pArr最大值 / 2
    }
    ```