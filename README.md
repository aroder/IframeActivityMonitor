Iframe Activity Monitor
--------------------------------------

Small library for monitoring user activity within an iframe in a cross domain scenario.
Same domain of origin policy limits the events that can be shared between iframes and
their containing document or window.

The IframeActivityMonitor allows tracking on an interval of when a user's mouse position
has changed within any iframe on the page.


Usage
--------------------------------------

	var myMonitor = new IframeActivityMonitor();

create an instance of the monitor object


	window.addEventListener('mousePositionChanged', function() {
	    console.log('Position changed!');
	}, false);

add an event listener to the window object to listen for

	monitor.start();

Start tracking. Any time the cursor is positioned over any iframe in the page, tracking will start. When to cursor moves the mouse out of the iframe, the tracking stops. As long as the cursor remains in the iframe, IframeActivityMonitor will check the cursor position on an interval, defined by `trackingInterval`. If the cursor position has changed, IframeActivityMonitor will dispatch the `mousePositionChanged` event.

	monitor.stop();

If ever necessary, you can stop tracking

	var myMonitor = new IframeActivityMonitor({ trackingInterval: 30000 });

Alternatively, you can call the constructor with an arguments object. The default settings will dispatch the `mousePositionChanged` every 1000 milliseconds, which could be way to frequent for your needs.

