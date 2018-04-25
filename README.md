/* Initially make sure that the gd-library is successfully added to the php ie by removing the comments line in the php.ini file.

we can chect it by phpinfo() commamd.

write <?php phpinfo() ?> check the output , which gives the information of whether gd-library is enabled or not.*/


<html>
<head><title>text on image</title>


</head>
<body>
	<form method="POST" action="<?php $_PHP_SELF ?>" enctype="multipart/form-data">
	<table>
		<tr>
			<td>
			upload image<input type="file" name="choose" />
			</td>
		</tr>
		<tr>
			<td>text input<input type="text" name="txfield"></td>
			<td>x-from left most<input type="number" name="xlocation" value="80"></td>
			<td>y-from top most <input type="number" name="ylocation" value="80"></td>
 		</tr>
 		<tr>
 			<td><input type="submit" name="submitit"></td>
 		</tr>
	</form></body> 
</html>
<?php
	
	if(isset($_POST['submitit']))
	{
		$filepath= "uploadedimages/" . $_FILES["choose"]["name"];
		if(move_uploaded_file($_FILES["choose"]["tmp_name"], $filepath))
		{
			
			$image = imagecreatefromjpeg('$filepath');
			$xpos=$_POST['xlocation'];
			$ypos=$_POST['ylocation'];
			$text=$_POST['txfield'];
			$fontSize=3;
			$angle=0;
			$color = imagecolorallocate($imagei, 0, 20, 50);
			imagestring($image, $fontSize, $xpos, $ypos,urldecode($text), $color);
			header('Content-type: image/jpeg');	
			imagejpeg($image,null,100);			

		}
		else
		{
			echo "ERROR";
		}
	}


?>
