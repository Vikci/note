# note

1. Convert image to base64 ()
```
function toDataURL(src, callback) {
  var img = new Image();
  img.crossOrigin = 'Anonymous';
  img.onload = function() {
    var canvas = document.createElement('CANVAS');
    var ctx = canvas.getContext('2d');
    var dataURL;
    canvas.height = this.naturalHeight;
    canvas.width = this.naturalWidth;
    ctx.drawImage(this, 0, 0);
    dataURL = canvas.toDataURL();
    callback(dataURL);
  };
  img.src = src;
}

toDataURL(
  http://upload.wikimedia.org/wikipedia/commons/4/4a/Logo_2013_Google.png,
  function(dataUrl) {
    console.log('RESULT:', dataUrl)
  }
)
```

2. Load the local image as blob via XMLHttpRequest and use the FileReader API to convert it to a dataURL:
```
function encodeImageFileAsURL() {
  var xhr = new XMLHttpRequest();
  xhr.open("GET", "public/assets/img/sf1.png", true); 
  xhr.responseType = "blob";
  xhr.onload = function (e) {
    console.log(this.response);
    var reader = new FileReader();
    reader.onload = function(event) {
       var res = event.target.result;
       console.log('encodeImageFileAsURL', res)
    }
    var file = this.response;
    reader.readAsDataURL(file)
  };
  xhr.send()
}

// ref: https://stackoverflow.com/questions/6150289/how-to-convert-image-into-base64-string-using-javascript
```
