# Overview

UTF-16 (16-bit Unicode Transformation Format) is a character encoding capable of encoding all 1,112,064 valid code points of Unicode (in fact this number of code points is dictated by the design of UTF-16). The encoding is variable-length, as code points are encoded with one or two 16-bit code units. UTF-16 arose from an earlier obsolete fixed-width 16-bit encoding now known as "UCS-2" (for 2-byte Universal Character Set),[1][2] once it became clear that more than 216 (65,536) code points were needed,[3] including most emoji and important CJK characters such as for personal and place names.[4]



## 比较下utf8，utf16，utf32 对字符a编码的输出结果
```java

import java.nio.charset.StandardCharsets;
import java.util.Arrays;

public class EncodingExample {
    public static void main(String[] args) {
        String str = "a";

        // UTF-8 Encoding
        byte[] utf8Bytes = str.getBytes(StandardCharsets.UTF_8);
        System.out.println("UTF-8: " + bytesToHex(utf8Bytes));

        // UTF-16 Encoding
        byte[] utf16Bytes = str.getBytes(StandardCharsets.UTF_16);
        System.out.println("UTF-16: " + bytesToHex(utf16Bytes));

        // UTF-32 Encoding (Java doesn't have a built-in UTF-32, so we need to handle it manually)
        try {
            byte[] utf32Bytes = str.getBytes("UTF-32");
            System.out.println("UTF-32: " + bytesToHex(utf32Bytes));
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // Helper method to convert bytes to a hexadecimal string
    private static String bytesToHex(byte[] bytes) {
        StringBuilder sb = new StringBuilder();
        for (byte b : bytes) {
            sb.append(String.format("%02x", b));
        }
        return sb.toString();
    }
}


```

Output:
``` 
UTF-8: 61
UTF-16: feff0061
UTF-32: 00000061

=== Code Execution Successful ===

```

### feff: 节序标记（Byte Order Mark, BOM）

在 Java 中使用 getBytes(StandardCharsets.UTF_16) 时，默认会在输出的字节数组中添加一个 BOM（字节序标记），这是 0xfeff。0xfeff 标记为大端序（Big Endian），意味着字节的高位在前。
如果不需要 BOM，可以使用 getBytes("UTF-16LE") 或 getBytes("UTF-16BE")。



# Unicode Escapes \u

Java:

Java 使用 \u 后跟四位十六进制数来表示 Unicode 字符。
例如，\u0041 表示字符 A。
```java

public class Main {
    public static void main(String[] args) {
        System.out.println("\u0041"); // 输出 A
    }
}


```

\u 前缀: 表示这是一个 Unicode 转义序列。

四位十六进制数: 紧跟在 \u 后面的四位数字（从 0000 到 FFFF）是 Unicode 代码点。每一个 Unicode 代码点表示一个字符。

例如：

- \u0041 = A
- \u03A9 = Ω
- \u263A = ☺
