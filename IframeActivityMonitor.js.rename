// Iframe Activity Monitor
// Small library for monitoring user activity within an iframe in a cross domain scenario.
// Same domain of origin policy limits the events that can be shared between iframes and
// their containing document or window.

// The IframeActivityMonitor allows tracking on an interval of when a user's mouse position
// has changed within any iframe on the page.

// USAGE:

// create an instance of the monitor object
                 // var myMonitor = new IframeActivityMonitor();

// add an event listener to the window object to listen for
					// window.addEventListener('mousePositionChanged', function() {
					    // console.log('Position changed!');
					// }, false);

// start tracking
					// monitor.start();


// if ever necessary, you can stop tracking
					// monitor.stop();


// alternatively, you can call the constructor with an arguments object
// var myMonitor = new IframeActivityMonitor({ trackingInterval: 30000 });


var IframeActivityMonitor = function(args) {
    args = args || {};
    
    // how often to compare current and old positions, in milliseconds
    var trackingInterval = args.trackingInterval || 1000;
    var oldPosition = {
        x: 0,
        y: 0
    };
    var trackingTimer;

    var eventHandlers = [];
    var start = function() {
        // add mouseover and mouseout listeners to every iframe
        var frames = document.getElementsByTagName('iframe');
        for (var i = 0; i < frames.length; i++) {

            // on mouseover, start tracking position within the iframe
            frames[i].addEventListener('mouseover', track, false);

            // on mouseout, stop tracking the mouse position within the iframe
            frames[i].addEventListener('mouseout', stopTracking, false);
        }
    };
    var stop = function() {
        var frames = document.getElementsByTagName('iframe');
        for (var i = 0; i < frames.length; i++) {
            frames[i].removeEventListener('mouseover', track, false);
            frames[i].removeEventListener('mouseout', stopTracking, false);
        }
    };
    var track = function(mouseEvent) {
        trackingTimer = setTimeout(function tracker() {
            //console.log('tracking');
            var frame = mouseEvent.target;
            var div = document.createElement('div');
            div.style.height = frame.clientHeight + 'px';
            div.style.width = frame.clientWidth + 'px';

            div.style.left = frame.offsetLeft + 'px';
            div.style.top = frame.offsetTop + 'px';
            div.style.position = 'absolute';
            //div.style.backgroundColor = '#000';
            div.innerHTML = '&nbsp;';
            document.body.appendChild(div);
            div.addEventListener('mouseover', function tracker2(mouseEvent) {
                var position = {
                    x: mouseEvent.clientX,
                    y: mouseEvent.clientY
                };
                
                // if the position is different than the old position, the
                // the mouse has moved within the iframe. Dispatch an event
                // on the window object
                if (position.x != oldPosition.x || position.y != oldPosition.y) {
                    dispatchEvent();
                }
                oldPosition = position;
                div.parentNode.removeChild(div);
            }, false);

        }, trackingInterval);
    };
    var stopTracking = function(mouseEvent) {
        clearTimeout(trackingTimer);
    };

    var dispatchEvent = function() {
        var evt = document.createEvent('Event');
        evt.initEvent('mousePositionChanged', true, true);
        window.dispatchEvent(evt);
    };

    return {
        start: start,
        stop: stop
    };
};

