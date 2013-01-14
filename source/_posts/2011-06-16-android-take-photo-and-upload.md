---
title: Android 拍照并上传图片到服务器源码
author: wahyd4
comments: true
layout: post
permalink: /2011/06/android-take-photo-and-upload/
categories:
  - 编程之美
tags:
  - android
  - java
  - web
---
> <span style="color: #ff0000;"><strong>更新：我已经把源码共享出来了，大家可以随便下载！</strong></span>
> 
> 最近帮老师做一个拍照上传的小android 应用。以前虽然看过这方面的东西，但是没有真正做过东西出来，这次老师要求在一个星期左右做出来，其实还是给了我不少压力，于是自己一边学习，一边写代码，同时在望山找了大量的东西，最初都没有解决这个问题。后面才慢慢解决这些问题。

下面是我写的源码给大家分享一下，说明一下，这些代码是调试完成可以运行的，当然这里没有提出全部的完整代码。如果各位需要的话，给我留言吧，我会通过邮箱发给大家的。 补充servlet端源代码：<a title="android上传图片到服务器server端servlet源码" href="http://toozhao.com/2011/06/android%E4%B8%8A%E4%BC%A0%E5%9B%BE%E7%89%87%E5%88%B0%E6%9C%8D%E5%8A%A1%E5%99%A8server%E7%AB%AFservlet%E6%BA%90%E7%A0%81/" target="_blank">Android上传图片到服务器Server端servlet源码</a>。这里的程序没有涉及服务器端使用的Servlet代码。稍后在贴出来给大家把。

<pre class="brush: java; title: ; notranslate" title="">// 选择拍照上传，获取bitmap 对象，并保存到sdcard中。
(takePhoto = (Button) findViewById(R.id.take_photo)) .setOnClickListener(new OnClickListener() {
@Override public void onClick(View v) {
//启动相机
Intent myIntent = new Intent( android.provider.MediaStore.ACTION_IMAGE_CAPTURE);
startActivityForResult(myIntent, ACTIVITY_IMAGE_CAPTURE);
} });
// 因为调用了startActivityForResult，调用相机后回执行这个方法
@Override protected void onActivityResult(int requestCode, int resultCode, Intent data) {
if (resultCode == RESULT_OK) {
//获取bitmap对象
Bundle dataBundle = data.getExtras();
Bitmap btp = (Bitmap) dataBundle.get("data");
data.putExtra(MediaStore.EXTRA_OUTPUT, btp);
/ 如果Junv文件夹不存在则创建文件夹，并将bitmap图像文件保存
dir = new File(ptoDir);
if (!dir.exists()) { dir.mkdirs(); Log.d("创建文件夹", "。。。。。。。。。。。成功"); }
 // 为文件随机产生文件名 
File tmpFile = new File(ptoDir, picName = System.currentTimeMillis() + ".jpg");
uploadFile = ptoDir + picName;
try {
// 将bitmap转为jpg文件保存
FileOutputStream fileOut = new FileOutputStream(tmpFile);
btp.compress(CompressFormat.JPEG, 100, fileOut);
} catch (FileNotFoundException e) {
//捕获异常
Log.d("File Saving", "fail.....");
}
// 将照片显示到程序中
ImageView myImage = (ImageView) findViewById(R.id.show_img);
//设置图片大小
btp = Bitmap.createScaledBitmap(btp, myImage.getWidth() - 10, myImage.getHeight() - 10, true);
//将图片加载到imageView中
myImage.setImageBitmap(btp);
myImage.setPadding(2, 2, 2, 2); } else { return; }
}
</pre>

执行完这个方法，我们通过bitmap对象将拍照所得已经显示在程序里面了，然后之所以将其保存为文件，是为了上传的方便。

然后下面是一个上传的图片的方法，大概就是将图片构建成流发送到是、服务器端，这个代码是使用的网上一个前辈的代码，这里不知道他的地址了，但是还是说明一下吧，并表示感谢。

<pre class="brush: java; title: ; notranslate" title="">//上传文件至Server的方法 
private void uploadFile(Bitmap btp) {
 String end = "rn";
 String twoHyphens = "--"; 
String boundary = "*****";
try {
URL url = new URL(actionUrl); 
HttpURLConnection con = (HttpURLConnection) 
url.openConnection();
//允许Input、Output，不使用Cache 
con.setDoInput(true);
con.setDoOutput(true);
con.setUseCaches(false);
//设置传送的method=POST 
con.setRequestMethod("POST");
//setRequestProperty
con.setRequestProperty("Connection", "Keep-Alive");
con.setRequestProperty("Charset", "UTF-8");
con.setRequestProperty("Content-Type", "multipart/form-data;boundary=" + boundary);
// 设置DataOutputStream 
DataOutputStream ds = new DataOutputStream(con.getOutputStream());
ds.writeBytes(twoHyphens + boundary + end);
ds.writeBytes("Content-Disposition: form-data; " + "name="file1";
filename="" + picName + """ + end); 
ds.writeBytes(end);
//取得文件的FileInputStream 
FileInputStream fStream = new FileInputStream(uploadFile);
// 设置每次写入1024bytes 
int bufferSize = 1024;
 byte[] buffer = new byte[bufferSize];
int length = -1;
// 从文件读取数据至缓冲区 
while ((length = fStream.read(buffer)) != -1)
{
 // 将资料写入DataOutputStream中  
ds.write(buffer, 0, length);
 }
ds.writeBytes(end);
ds.writeBytes(twoHyphens + boundary + twoHyphens + end);
//close streams
fStream.close();
ds.flush();
// 取得Response内容 
InputStream is = con.getInputStream();
int ch;
StringBuffer b = new StringBuffer();
 while ((ch = is.read()) != -1) {
 b.append((char) ch); }
// 将Response显示于Dialog 
showDialog("上传成功" + b.toString().trim());
// 关闭DataOutputStream 
ds.close();
 } catch (Exception e) { 
showDialog("上传失败" + e);
 } }
// 显示Dialog的method
private void showDialog(String mess) 
{ 
new AlertDialog.Builder(this).setTitle("Message").setMessage(mess) .setNegativeButton("确定", new DialogInterface.OnClickListener() {
 public void onClick(DialogInterface dialog, int which) { } }).show();
 }
</pre>

请看我们的第一篇文章：<a href="http://toozhao.com/2011/06/android%E4%B8%8A%E4%BC%A0%E5%9B%BE%E7%89%87%E5%88%B0%E6%9C%8D%E5%8A%A1%E5%99%A8server%E7%AB%AFservlet%E6%BA%90%E7%A0%81/" target="_blank">Android上传图片到服务器Server端servlet源码</a>。

> android端和web 端源码下载：http://115.com/file/bevc7e16#uploadsome.rar
