# touchmeJS

## About

A simple javascript library for adding touch events to your app, provides mouse fallback for greater ease.

## Usage

#### In the Browser:

    <script src='touchme.js'></script>`

#### CommonJS

    require('/touchme');`


#### Instantiating

```javascript
touchme(args); //returns true if on touch device, false otherwise
```

##### where args is an object to override default arguments, the defaults are as follows:
    {
        swipeThreshold: 80,    //the minimun distance required for a 'swipe' event to fire
        tapThreshold: 200,     //the time in milleseconds to wait for a dbltap
        holdThreshold: 550,    //the time in milliseconds required for a 'hold' event to fire
        precision: 45,         //the boundary for all tap events
        onlyTouch: false,      //when set to true, events only fire on touch device
        swipeOnlyTouch: false, //when set to true, swipe events only fire on touch device,
        nTap: false            //still experimental, if the users clicks >=3 taps within tap threshold, nTap is fired containing how many taps occured.
    }
___


## All events are called in the following manner:

```javascript
el.addEventListener(evtName, function(data){});
```
####where evtName is one of the following events:

### tap, dbltap
```javascript
data : {
  x: x-position of tap,
  y: y-position of tap
}
```

### swipeup, swiperight, swipedown, swipeleft
```javascript
data : {
  x: x-position of tap,
  y: y-position of tap,
  direction.radians: direction of swipe in radians,
  direction.degrees: direction of swipe in degrees,
  distance.x: distance of swipe in pixels along the x axis,
  distance.y: distance of swipe in pixels along the y axis
}
```

### hold
```javascript
data : {
  x: x-position where hold was initiated,
  y: y-position where hold was initiated,
}
```
### drag
#### fired when item is being held, and target is moving (touchmove, mousemove) 

```javascript
data : {
  x: x-position of cursor,
  y: y-position of cursor,
}
```

### holdrelease
```javascript
data : {
  originalX: x-position where hold was initiated,
  originalY: y-position where hold was initiated,
  lastX: x-position where hold was ended,
  lastY: y-position where hold was ended
}
```

### pinch
#### binds to touch move, though an initial 'pinchState' is recorded if two touches are detected, the pinch event only fires when the user is moving, based on the resolution given in the defaults
```javascript
data : {
  initialPinch  :{
    distance : the distance between two touches of initial pinch,
    'touch0' : {
      x: x-coord of first touch,
      y: y-coord of first touch,
    },
    'touch1' : {
      x: x-coord of second touch
    }
  },
  touchPoints : {
    distance : the distance between the moved pinch gesture,
    'touch0' : {
      x: x-coord of first touch,
      y: y-coord of first touch,
    },
    'touch1' : {
      x: x-coord of second touch
    }
  },
  distance : the distance between the moved pinch gesture, for easy access
  midpoint : the midpoint between the moved pinch gesture
```
### Things upcoming
- [x] pinch gesture
- [ ] implement a 'multiple hold' function for dragging and dropping multiple items simultaneously
- [ ] phantomJS tests
