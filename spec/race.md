## hierarchy

- [race](#race-object)
  - [ranking](#ranking-object)
  - [task](#task-object)
    - [turnpoints](#turnpoint-object)
    - [route](#route-object)

## datatypes
```
STRING    := sequence of ASCII characters
DATE      := STRING complying to ISO 8601 date format "YYYY-MM-DD"
TIMESTAMP := STRING complying to ISO 8601 extended time format "hh:mm:ss"
NUM       := numerical value
BOOL      := true or false
```

## race object

```js
"properties" : {
  "n_snaps" : NUM,
},
"task" : {},        // task object
"ranking" : {},     // ranking object
"snaps" : {
  TIMESTAMP : {
    ID : {
      "lat" : NUM,
      "lon" : NUM,
      "alt" : NUM,
      "status" : STRING, // FLYING, LANDED (more analysis TODO)
      "goal_distance" : NUM,
    }
  }
}
```

## task object
```js
{
  "date" : DATE,      // OPTIONAL - date of task
  "status" : STRING,  // OPTIONAL - OK, PREVISIONAL, STOPPED, CANCELLED (maybe object with time of stop ?)
  "style" : STRING,   // OPTIONAL - RACE, ELAPSED, CLOCK
  "valid" : BOOL      // OPTIONAL - task validity check (to be defined)
  "takeoff" : {},     // REQUIRED - turnpoint object of the takeoff
  "sss" : {},         // REQUIRED - turnpoint object of the sss
  "ess" : {},         // REQUIRED - turnpoint object of the ess
  "goal" : {}         // REQUIRED - turnpoint object of the goal
  "turnpoints" : [],  // REQUIRED - all turnpoints objects in race order
  "route" : {},       // OPTIONAL - route object
 }
```

## turnpoint object 
```js
{
  "name" : STRING,        // REQUIRED - ("D01")
  "description" : STRING, // OPTIONAL - description of the turnpoint ("Pic des Moros")
  "lat" : NUM,            // REQUIRED - latitude
  "lon" : NUM,            // REQUIRED - longitude
  "radius" : NUM,         // OPTIONAL - radius in meters
  "alt" : NUM,            // OPTIONAL - altitude in meters
  "agl" : NUM,            // OPTIONAL - altitude above ground in meters
  "open" : TIMESTAMP,     // OPTIONAL - opening time
  "close" : TIMESTAMP,    // OPTIONAL - closing time
  "direction" : STRING,   // OPTIONAL - "ENTER" or "EXIT" 
  "is_line" : BOOL        // OPTIONAL - is turnpoint a line or a cylinder ?
  "first_tag" : TIMESTAMP // OPTIONAL - time of first tag during race
  "role" : STRING,        // REQUIRED - TAKEOFF, SSS, TURNPOINT, ESS, GOAL
  "source" : STRING,      // OPTIONAL - source file of this turnpoint
}

```
## route object
```js
{
  "center_dist" : NUM, // distance via centers in meters
  "opt_dist" : NUM,    // distance via optimal route in meters
  "center_legs" : [],  // distance of consecutive legs via centers in meters
  "opt_legs" : [],     // distance of consecutive legs via optimal route in meters
  "opt_points" : [],   // turnpoints objects of the optimal route
}
```

## ranking object

```js
"scoring" : {},      // scoring object (TODO)
"pilots" : [         // list of pilots, sorted by decreasing score
  "name": STRING,    // pilot name
  "id": STRING,      // flight filename
  "in_goal" : BOOL,
  "distance": NUM,
  "time": TIMESTAMP, 
  "points": NUM      // according to scoring
],
```

## references
 *  [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)