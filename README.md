<h1>limited-calls</h1>

Wraps a function so it can only be called once during a set delay time.

--

I wrote this to limit the amount of calls to an event handler to a maximum of 1 call every 100 milliseconds.


**Usage**:


>Install with npm: `npm install --save limited-calls`


```javascript
const limitedCalls= require 'limited-calls'

const show= ( ...text ) => console.log( 'showing:', ...text );

// wrap the show function, allowing only calling once a second
let myShow= limitedCalls( show, 1000 );

myShow( 'hello', 'world!' );
// showing: hello world!
myShow( 'ignored not showing..' );
myShow( 'ignored not showing..' );

setTimeout( () => {
	myShow( 'hello again!' );
	// hello again!
	myShow( 'ignored not showing..' );
}, 2000 );

// when calls to the function are made during the delay time,
// the last call is saved and called directly after the delay expires.
// if you want to also ignore this last pending call, you can
// pass true as a third parameter to set "ignorePending"
myShow= limitedCalls( show, 1000, true );
```

<h3>license</h3>

MIT