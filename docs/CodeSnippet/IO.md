---
lang: "zh-CN"
title: "IO流"
description: "这个项目将会记录学习过程中的知识点！"
---

## 文件操作

### 读取文件

```java
public static String readNode(File file,String fileType){
    String str="";
    String resultStr="";
    /*如果f为文件并且文件后缀为fileType*/
    if(file.isFile()&&file.getName().endsWith("."+fileType)){
        try {
            InputStream is=new FileInputStream(file);
            Reader in=new InputStreamReader(is);
            BufferedReader reader=new BufferedReader(in);
            while((str=reader.readLine())!=null){
                resultStr+=str;
            }
            reader.close();
            in.close();
            is.close();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    System.out.println("resultStr:::\n"+resultStr);
    return resultStr;
}
```

### 写文件

```java
public static void writeNode(String dosPath,String data){
    try {
        OutputStream os=new FileOutputStream(dosPath);
        Writer osw=new OutputStreamWriter(os, "gbk");
        PrintWriter out=new PrintWriter(osw);
        out.print(data);
        out.close();
        osw.close();
        os.close();
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    } catch (UnsupportedEncodingException e) {
        e.printStackTrace();
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

### 清除文件

```java
public static void delNote(File f) {
    String str = "";
    String rootDirectory = "d";
    if ((f.isFile()) && (f.getName().endsWith(".java"))) {
        System.out.println(f.getName());
        try {
            InputStream is = new FileInputStream(f);
            Reader in = new InputStreamReader(is);
            BufferedReader reader = new BufferedReader(in);

            String file = rootDirectory
                    + f.getPath().substring(1, f.getPath().length());
            System.out.println("file:::" + file);
            FileOutputStream fos = new FileOutputStream(file);
            OutputStreamWriter osw = new OutputStreamWriter(fos, "gbk");
            PrintWriter out = new PrintWriter(osw);

            while ((str = reader.readLine()) != null) {
                Pattern pattern2 = Pattern.compile("/\\*(.*?)\\*/", 32);
                Matcher matcher2 = pattern2.matcher(str);
                str = matcher2.replaceAll("");
                out.println(str);
            }
            is.close();
            in.close();
            reader.close();
            out.close();
        } catch (IOException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    } else if (f.isDirectory()) {
        String resultPath = rootDirectory
                + f.getPath().substring(1, f.getPath().length());
        File fileDemo = new File(resultPath);
        fileDemo.mkdir();
        File[] fs = f.listFiles();
        for (int i = 0; i < fs.length; i++) {
            File file = fs[i];
            delNote(file);
        }
    }
    System.out.println("修改完毕\n存放目录在 " + rootDirectory.toUpperCase() + "盘！");
}
```
