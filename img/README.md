# all of the images are loaded
```

let images =["/background.jpg","/logo.png","/newtab.png"];

function imgLoad(url) {
  return new Promise(function(resolve, reject) {
    var img = new Image();
    img.src = url;
    img.onload = function() {
      resolve(img);
    }
    img.onerror = reject
  });
}

// map an array of promises calling imgLoad() for each url
let imageLoadpromises = images.map(imgLoad);

Promise.all(imageLoadpromises ).then(function(images){
   //images is array of image elements from above
   // do something here , they have all loaded

}).catch(function(err){ 
     console.log('One or more images did not load')
});
```
