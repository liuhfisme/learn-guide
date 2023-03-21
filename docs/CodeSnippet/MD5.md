# MD5加密算法
## 1、生成32位加密字符串
```java
public static String digest(String s) {
    MessageDigest md5 = DigestUtils.getMd5Digest();
    byte[] digest = md5.digest(s.getBytes(StandardCharsets.UTF_8));
    StringBuffer hexValue = new StringBuffer();
    for (int i = 0; i < digest.length; i++) {
        int val = digest[i] & 0xff;
        if (val < 16) {
            hexValue.append("0");
        }
        hexValue.append(Integer.toHexString(val));
    }
    return hexValue.toString();
}

public static void main(String[] args) {
    String appid = "f90882fb885046e1ae03aae8785dfe60";
    String appkey = "932d5febf6d0d4173482922029483d1e";
    long time = System.currentTimeMillis() / 1000;
    String s = appid + time + appkey;
    System.out.println(appid + time + appkey);
    System.out.println(time);
    System.out.println(digest(s));
    System.out.println( DigestUtils.md5Hex(appid + time + appkey));
}
```