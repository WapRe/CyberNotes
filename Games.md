<h2>Cetus</h2>
<p>
  Browser plugin that works for Firefox and Chrome, allowing you to explore the memory space of Web Assembly games that run in your browser.<br>
  Tool to easily find any piece of data stored in memory and modify it if needed.<br> 
  Let you modify a game's compiled code and alter its behaviours if you want<br>
</p>
<h3>Firefox installation</h3>
<p>
  To run Cetus on Firefox, you will need to load it as a temporary extension since it isn't available on the add-ons website.<br>
  To do this, open Firefox and type about:debugging in the address bar.<br>
  Once in there, go to This Firefox, where you'll find a button to load temporary add-ons.<br>
  Temporary add-ons will only be loaded for as long as the browser remains open, so you'll need to load it again if you close it for some reason.<br>
  To load the extension, you will need to browse to the directory where you downloaded and extracted Cetus and select the manifest.json file inside the main folder and click OK.
</p>
<h3>Chrome installation</h3>
<p>
  To install Cetus on Chrome, type chrome://extensions in your address bar.<br>
  This will take you to the extensions manager. You will need to enable the Developer mode, enabling additional buttons to load the extension.<br>
  Click the Load unpacked button and point to the directory where you uncompressed the plugin.<br>
  This will open an explorer window where you'll need to go to the directory where Cetus was uncompressed, and press the Open button from there without selecting any file<br>
  Once you are done, you should see Cetus loaded in your extensions<br>
</p>
<h3>Options:</h3>
<p>
  <ul>
    <li>i32 : when you want to introduce a regular integer (32-bit-integer) in <b>Value Type</b></li>
    <li>f32/f64 : search for numbers with decimals (usually called floats)</li>
    <li>ascii/utf-8/bytes : search for strings</li>
  </ul>
<h3>Comparison operators:</h3>
  <ul>
    <li>EQ: Find all memory addresses with contents that are <b>equal</b> to our inputted value.</li>
    <li>NE:Find all memory addresses with contents that are <b>not equal</b> to our inputted value.</li>
    <li>LT: Find all memory addresses with contents that are <b>lower</b> than our inputted value.</li>
    <li>GT: Find all memory addresses with contents that are <b>greater</b> than our inputted value.</li>
    <li>LTE: Find all memory addresses with contents that are <b>lower than or equal</b> to our inputted value.</li>
    <li>GTE: Find all memory addresses with contents that are <b>greater than or equal</b> to our inputted value.</li>
  </ul>
</p>
