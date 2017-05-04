Collection of handy dandy (javascript) formulas and algorithms for use in game development. They can mostly be ported to other languages easily.

### Why?
Granted, there's a gazillion of libraries out there containing many a handy method. But many times I don't want a library. I just want a quick function or method. So this aims to be a big collection of them. Please contribute! 

## Conversion / transcoding

## Position determination
```
     /**
      * returns the distance between two lat long coordinates
      * (uses degToRad and radToDeg functions below)
      */
     function latlongdist(lat1, long1, lat2, long2) {
         var theta = long1 - long2;
         var miles = (Math.sin(degToRad(lat1)) * Math.sin(degToRad(lat2))) + (Math.cos(degToRad(lat1)) * Math.cos(degToRad(lat2)) * Math.cos(degToRad(theta)));
         miles = radToDeg(Math.acos(miles)) * 60 * 1.1515;
         var feet = miles * 5280;
         var yards = feet / 3;
         var km = miles * 1.609344;
         var meters = km * 1000;
         return {
           'miles':miles,
           'feet':feet,
           'yards':yards,
           'km':km,
           'meters':meters
         }; 
     }
```

## Variables

### strings
```
     /**
      * return a random, unique-ish id
      */
     function guid() {
          return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
              var r = Math.random()*16|0, v = c == 'x' ? r : (r&0x3|0x8);
              return v.toString(16);
          });
     }
```

### numbers
```
     /**
      * return random int in range
      */
     this.randInt = function (min, max) {
         return Math.floor(Math.random() * (max - min + 1)) + min;
     }
     
     
     /**
      * return random float in range
      */
     function randFloat (min, max) {
         return Math.random() * (max - min) + min;
     }
     
     /**
      * degrees to radians
      */
     function degToRad(deg) {
          return deg*(Math.PI/180);
     }

     /**
      * radians to degrees
      */
     function radToDeg(rad) {
          return rad/(Math.PI/180);
     }

     /**
      * returns the fraction behind the flaoting point of a float
      */
     function returnFloat(n) {
          return n - Math.floor(n);
     }

     /**
      * returns a value between 0 and 1 that represents the given value in the given range
      */
     function normalize(value, minimum, maximum) {
          return (value - minimum) / (maximum - minimum);
     }

     /**
      * returns the value in the given range for a representing normalized value
      * (it's normalize, but the other way around)
      */
     function interpolate (normValue, minimum, maximum) {
          return minimum + (maximum - minimum) * normValue;
     }    
     
     /**
      * returns the mapped value in range 2, given value 1 in range 1
      * (it's normalize, and than interpolate in a new range)
      */
     function map(value, min1, max1, min2, max2) {
          return this.interpolate( this.normalize(value, min1, max1), min2, max2);
     } 
```

### arrays

```
     /**
      * return randomized array
      */
     function randomized(arr) {
          var array = arr.slice(0);
          for (var i = array.length - 1; i > 0; i--) {
              var j = Math.floor(Math.random() * (i + 1));
              var temp = array[i];
              array[i] = array[j];
              array[j] = temp;
          }
          return array;
     }


     /**
      * check if value exists in array
      */
     function inArray(val, arr, returnIndex) {
          returnIndex = typeof returnIndex !== 'undefined' ? returnIndex : false;

          var len = arr.length;
         for(var i = 0; i < len; i++) {
             if(val == arr[i]) 
                  return returnIndex ? i : true;
         }
          return false;
     }
```

## DOM

```
     /**
      * returns size of window in vanilla js
      */
     function windowsize(){
          var w = 0;var h = 0;
          if(!window.innerWidth){
              if(!(document.documentElement.clientWidth == 0)){
                  w = document.documentElement.clientWidth;
                  h = document.documentElement.clientHeight;
              } else {
                  w = document.body.clientWidth;
                  h = document.body.clientHeight;
              }
          } else {
              w = window.innerWidth;
              h = window.innerHeight;
          }
          return {width:w,height:h};
     }
```
