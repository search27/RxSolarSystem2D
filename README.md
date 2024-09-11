# RxSolarSystem2D
RxSolarSystem2D

* Degree To Time
* Time To Degree
* 24 Hours Devided By 360 Degree

Support By [ Cloud Rx (<a href='https://rxapis.com'>https://rxapis.com</a>) ].
* Testing is available until the end of the year.

## Table of Contents

- [Rx Solar System 2D](#rx-solar-system-2d)
    - [Steps]
    - [Default Function](#default-function)
    - [RxStar](#rx-star)
    - [RxSolarSystem2D](#rx-solar-system-2d)
    - [RxSolarHTML](#rx-solar-html)


## Rx Solar System 2D
* Rx Solar System 2D For Canvas


### Steps
* Folder - steps
** step1 : Create Stars
** step2 : Create Interface
** step2-1 : Date To Degree
** step3 : Multiple Stars


### Default Function

* Create Canvas
* func CreateCanvas : (target, canvasCount, resize) return (Array) canvas

```javascript
const canvas = RxLongShadow2D.CreateCanvas(document.body, 2, true);
```

* func DateToTime : (Date) return { hh, min, sec }
```javascript
const time = SolarSystem2D.DateToTime(new Date());
```

* func DateToDegree : (Date) return degree
```javascript
const degree = SolarSystem2D.DateToDegree(new Date());
```

* func DegreeToDate : (Date) return degree
```javascript
const degree = SolarSystem2D.DateToDegree(new Date());
const dt = SolarSystem2D.DegreeToDate(new Date());
```

* func DateToTimeString : (Date) return String Time (ex : "13:12:59")
```javascript
const timeString = SolarSystem2D.DateToTimeString(new Date());
```

* func PercentageToDate : (percentage) return Date
```javascript
// 12 Hours = 50%
// 24 Hours = 100%
const percentage = 10 / 100;
const dt = SolarSystem2D.PercentageToDate(percentage);
```


### RxStar
* Constructor
* func update :
* func draw : (ctx)
* func SetProperties : (property)
* func SetDegree : (degree - Number)
* func SetColor : (String)
* func SetRadius : (Number)
* func SetCentroid : (Array<x,y>)
* func SetDistance : (Number)
* func SetImage : (String)
* func SetVisualize : (bool);

* func GetDegree : () return degree - Number;
* func GetColor : () return String;
* func GetRadius : () return Number;
* func GetCentroid : () return Array<x,y>;
* func GetDistance : () return Number;
* func GetPosition : () return { x, y } - Object;
* func GetImage : () return String;


```javascript
const sun = {
    label : 'Sun',
    centroid : [window.innerWidth / 2, window.innerHeight / 2],
    radius : 100,
    distance : 300,
    degree : 180,
    color : 'rgba(0, 255, 255, 1)',
    image : './images/sun.webp',
};

const CreateStar = function(star){
    const st = new SolarSystem2D.RxStar(star.centroid, star.radius, star.distance, star.color);
    st.SetDegree(star.degree);
    st.SetProperties(star);
    if(star['image'] && star['image'] !== ''){
        const img = new Image();
        img.src = star['image'];
        img.addEventListener('load', function(){ st.SetImage(img); });
    }
    return st;
}

```

### RxSolarSystem2D

* Constructor
* func update :
* func draw : (ctx)
* func SetStars : (stars)                   // Overwrite
* func AddStar : (star)                     // Add
* func SetVisualize : (bool)
* func SetRxSolarHTML : (rxSolarHtml)
* func FindStarFromLabel : (label - String) return RxStar
* func GetAllStars : () return Array<RxStar>


```javascript

// Default Properties
const sun = {
    label : 'Sun',                                                  // Label Should be primary key
    centroid : [window.innerWidth / 2, window.innerHeight / 2],     // Center
    radius : 100,                                                   // Circle Size
    distance : 300,                                                 // How far Is This From Centroid
    degree : 180,                                                   // Initial Degree
    color : 'rgba(0, 255, 255, 1)',
    image : './images/sun.webp',                                    // Optional
};
const moon = {
    label : 'Moon',                                                 // Label Should be primary key
    centroid : [window.innerWidth / 2, window.innerHeight / 2],
    radius : 50,
    distance : 100,
    degree : 0,
    color : 'rgba(138, 213, 255, 1)',
    image : './images/moon.webp',
}


const init = () => {

    // Create Canvas
    const canvas = SolarSystem2D.CreateCanvas(document.body, 1, true);

    // Create Rx Solar System 2D
    const rxSolar2D = new SolarSystem2D.RxSolarSystem2D();

    // Add Stars Or Set Stars
    // rxSolar2D.AddStar(sun);
    // rxSolar2D.AddStar(moon);

    // Overwrite
    rxSolar2D.SetStars([sun, moon]);


    // Visualize Centroid, Vector, Label
    rxSolar2D.SetVisualize(true);


    const anime = function(){
        canvas.forEach(each => { each.ctx.clearRect(0, 0, each.canvas.width, each.canvas.height); });
        rxSolar2D.update();
        rxSolar2D.draw(canvas[0].ctx);

        // Get Star By Label
        const sunStar = rxSolar2D.FindStarFromLabel('Sun');
        const moonStar = rxSolar2D.FindStarFromLabel('Moon');
        sunStar.SetDegree(sunStar.GetDegree() + 1);
        moonStar.SetDegree(moonStar.GetDegree() + 1);

        requestAnimationFrame(anime);
    }
    anime();
}

init();

```

### RxSolarHTML
* Create Inteface
* Constructor


```javascript

let turnOnOff = true;
let rxSolar2D;

// Button Interface
// Define Buttons
const globals = {
    time : new Date(),
    className : 'rx-solar-html',
    buttons : [
        {
            name : 'cursor',
            image : '../images/i_cursor.webp',
            func : ()=>{
                // Define Here
                turnOnOff = !turnOnOff;
                rxSolar2D.SetVisualize(turnOnOff);
            }
        },
        {
            name : 'time',                                        // [ time ] Is Key By Auto Progress
            image : '../images/i_clock.webp',                     // Optional
            func : ()=>{
                console.log('clock');
            }
        },
    ]
};

// Create Rx Solar System 2D
rxSolar2D = new SolarSystem2D.RxSolarSystem2D();

// Add Interface - And Done
const solarHTML = new SolarSystem2D.RxSolarHTML(document.body, globals);
rxSolar2D.SetRxSolarHTML(solarHTML);


```

<img width="1659" alt="스크린샷 2024-09-11 오후 8 14 26" src="https://github.com/user-attachments/assets/b5e71201-0739-4423-87e5-5667e5447850">
<img width="1659" alt="스크린샷 2024-09-11 오후 8 13 56" src="https://github.com/user-attachments/assets/36b64e57-c159-40b8-b9c0-a50242c5e2f3">



