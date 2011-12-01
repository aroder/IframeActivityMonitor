Iframe Activity Monitor
--------------------------------------

Small library for monitoring user activity within an iframe in a cross domain scenario.
Same domain of origin policy limits the events that can be shared between iframes and
their containing document or window.

The IframeActivityMonitor allows tracking on an interval of when a user's mouse position
has changed within any iframe on the page.


USAGE:

create an instance of the monitor object

'var myMonitor = new IframeActivityMonitor();'

add an event listener to the window object to listen for

	window.addEventListener('mousePositionChanged', function() {
	    console.log('Position changed!');
	}, false);


start tracking

'monitor.start();'


if ever necessary, you can stop tracking

	monitor.stop();


alternatively, you can call the constructor with an arguments object
var myMonitor = new IframeActivityMonitor({ trackingInterval: 30000 });