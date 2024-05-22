<h1>JavaScript QR Code and Barcode Scanner</h1>
<p>This project provides a JavaScript-based QR code and barcode scanner that can be easily integrated into any HTML-based webpage. It supports scanning using the camera on both HTTPS and localhost environments, while also working on HTTP (though HTTP does not support camera access due to security reasons).</p>
<h2>Features</h2>
<ul>
    <li><strong>QR Code Scanning</strong>: Quickly scan and decode QR codes.</li>
    <li><strong>Barcode Scanning</strong>: Supports various barcode formats.</li>
    <li><strong>Camera Access</strong>: Utilizes the device's camera for scanning (HTTPS and localhost only).</li>
    <li><strong>Cross-Browser Compatibility</strong>: Works on major browsers that support camera access.</li>
    <li><strong>Two Modes</strong>:
        <ul>
            <li><strong>External Mode</strong>: Open scanner in a new window on button click.</li>
            <li><strong>Embedded Mode</strong>: Embed scanner within the page using an iframe with continuous multiple scanning capability.</li>
        </ul>
    </li>
</ul>
Link:
<pre><code>
https://tihloh.github.io/codescanner
</code></pre>
<hr>
<h2>External Mode</h2>
<p>
On button click, it will automatically activate the scanner. On scan success, it will return to the reference page with the result as a GET parameter "result". If canceled, it will return without the result.
<p>
<h3>Example #1: Using only html and javascript</h3>
<pre>
<code>
&lt;h3 id="result"&gt;Result: &lt;/h3&gt;
&lt;button onclick="openScanner()"&gt;Open Scanner&lt;/button&gt;
&lt;script&gt;
    function openScanner(){
        window.location.href = 'https://tihloh.github.io/codescanner?url=' + encodeURIComponent(window.location.href);
    }
    window.onload = (event) =&gt; {
        const urlParams = new URLSearchParams(window.location.search);
        const result = decodeURIComponent(urlParams.get('result'));
        document.getElementById('result').innerText = "Result: " + result;
    };
&lt;/script&gt;
</code>
</pre>
Check out this <a href="https://tihloh.github.io/codescanner/demo1.html" target=blank_>LIVE DEMO</a>!
<h3>Example #2: Using PHP</h3>
<pre>
<code>
&lt;?php	
    if (isset($_REQUEST['result'])){
    	$result=$_REQUEST['result'];
    	echo "Scan result: ".$result;
    }
?&gt;
&lt;button onclick="openScanner()"&gt;Open Scanner&lt;/button&gt;
&lt;script&gt;
    function openScanner(){
        window.location.href = 'https://tihloh.github.io/codescanner?url=' + encodeURIComponent(window.location.href);
    }
&lt;/script&gt;
</code>
</pre>
<h3>Example #3</h3>
With "pcode" param to compare the code if the same as the previous scan, if the code is different, saves to database, then loads the scanner again for the next code.
<pre>
<code>
&lt;?php	
    if (isset($_REQUEST['qrvalue'])){
        $qrvalue=$_REQUEST['qrvalue'];
        $pcode=@$_REQUEST['pcode'];
        if($pcode!=$qrvalue){
            $q="UPDATE tblemps SET scancode='$qrvalue' WHERE id='$user_id'";
            if (!$mysqli-&gt;query($q)) {
                $error = $mysqli-&gt;error;	
            }
        }
        $url = (empty($_SERVER['HTTPS']) ? 'http' : 'https') . '://$_SERVER[HTTP_HOST]/budget/dashboard?pcode=$qrvalue';
?&gt;
        &lt;script&gt;window.location.href = 'https://tihloh.github.io/codescanner?url=' + encodeURIComponent("&lt;?=$url;?&gt;");&lt;/script&gt;
&lt;?php
        exit;
    }
?&gt;
&lt;button onclick="openScanner()"&gt;Open Scanner&lt;/button&gt;
&lt;script&gt;
    function openScanner(){
        window.location.href = 'https://tihloh.github.io/codescanner?url=' + encodeURIComponent(window.location.href);
    }
&lt;/script&gt;
</code>
</pre>
<hr>
<h2>Embedded Mode</h2>
<h3>Example</h3>
Embedded Scanner on iFrame
<pre><code>
&lt;h1&gt;Embedded QR-Code/Barcode Scanner&lt;/h1&gt;
&lt;iframe src="https://tihloh.github.io/codescanner?iframe=1" id="myIframe" width="100%" height="300vp" style="-webkit-transform:scale(1);-moz-transform-scale(1);border:none;"&gt;&lt;/iframe&gt;
&lt;h3 id="result"&gt;Waiting...&lt;/h3&gt;
&lt;script&gt;
    	function handleMessage(event) {
    	    	document.getElementById('result').innerText = event.data.message;
    	}
    	window.addEventListener('message', handleMessage);
&lt;/script&gt;
</code></pre>
Check out this <a href="https://tihloh.github.io/codescanner/demo2.html" target=blank_>LIVE DEMO</a>!
