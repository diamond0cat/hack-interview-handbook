
Given a string in compressed form, decompress it to the original string. 
The adjacent repeated characters in the original string are compressed 
to have the character followed by the number of repeated occurrences.

Assumptions

The string is not null

The characters used in the original string are guaranteed to be ‘a’ - ‘z’

There are no adjacent repeated characters with length > 9

Examples

“a1c0b2c4” → “abbcccc”


```java
public class Solution {
  public String decompress(String input) {
     // left --> right : decode short
     // right --> left: decode long
     if (input.isEmpty()) {
       return input;
     }
     char[] arr = input.toCharArray();
     return decodeLong(arr, decodeShort(arr));
     
  }
  // return new length after decodeShort
  private int decodeShort(char[] input) {
   int end  = 0;
   for (int i = 0; i < input.length ;i+=2) {
     int digit = getDigit(input[i + 1]);
     if (digit >= 0  && digit <= 2){
       for (int j = 0; j < digit; j++) {
         input[end++] = input[i];
       }
     } else {
       input[end++] = input[i];    // keep long code as original
       input[end++] = input[i + 1];
     }
   }
   
   return end; 
  }
  private int getDigit(char c) {
    return c - '0';
  }
  private String decodeLong(char[] input, int length) {
    int newLength = length;
    // calculate new length
    for (int i = 0; i < length; i++) {
      int digit = getDigit(input[i]);
      if (digit > 2 && digit <= 9) {
          newLength += digit - 2;
      }
    
    }
    char[] result = new char[newLength];
    int end = newLength - 1;
    for (int i = length - 1; i >= 0; i--) {
      int digit = getDigit(input[i]);
      if (digit > 2 && digit <= 9) {
        i--;
        for (int j = 0; j < digit; j++) {
          result[end--] = input[i];
        }
      } else {
        result[end--] = input[i];
      }
    }
    return new String(result);
  }
}

```