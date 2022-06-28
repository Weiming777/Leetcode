1. 去除开头和结尾的空格

   ```java
   // remove leading spaces
       s = s.trim();
   ```

2. 按照给定的表达式进行拆分字符串

   ```java
   public class Test {
       public static void main(String args[]) {
           String str = new String("Welcome-to-Runoob");
    
           System.out.println("- 分隔符返回值 :" );
           for (String retval: str.split("-")){
               System.out.println(retval);
           }
    
           System.out.println("");
           System.out.println("- 分隔符设置分割份数返回值 :" );
           for (String retval: str.split("-", 2)){
               System.out.println(retval);
           }
    
           System.out.println("");
           String str2 = new String("www.runoob.com");
           System.out.println("转义字符返回值 :" );
           for (String retval: str2.split("\\.", 3)){
               System.out.println(retval);
           }
    
           System.out.println("");
           String str3 = new String("acount=? and uu =? or n=?");
           System.out.println("多个分隔符返回值 :" );
           for (String retval: str3.split("and|or")){
               System.out.println(retval);
           }
       }
   }
   ```

   ```java
   - 分隔符返回值 :
   Welcome
   to
   Runoob
   
   - 分隔符设置分割份数返回值 :
   Welcome
   to-Runoob
   
   转义字符返回值 :
   www
   runoob
   com
   
   多个分隔符返回值 :
   acount=? 
    uu =? 
    n=?
   ```

tip：

"\s+"详解
正则表达式中\s匹配任何空白字符，包括空格、制表符、换页符等等, 等价于[ \f\n\r\t\v]

\f -> 匹配一个换页
\n -> 匹配一个换行符
\r -> 匹配一个回车符
\t -> 匹配一个制表符
\v -> 匹配一个垂直制表符
而“\s+”则表示匹配任意多个上面的字符。另因为反斜杠在Java里是转义字符，所以在Java里，我们要这么用“\\\s+”.


