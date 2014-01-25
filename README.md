# LCZoomTransition

A custom UIViewController animated and interactive transition for use in master detail apps that uses a zoom in effect when going from master to detail and a zoom out effect when going back to the master view.

## Requirements

* iOS 7.0 or later.
* ARC memory management.

## Usage

The easiest way to install it is by copying the following to your project:

* LCZoomTransition.h
* LCZoomTransition.m

* In your master view controller, initialize an instance of an LCZoomTransition, passing it your navigation controller:

      self.zoomTransition = [[LCZoomTransition alloc] initWithNavigationController:self.navigationController];

* Add a property to your detail view controller to be able to make the transition a gesture target:

      @property (nonatomic, strong) id<LCZoomTransitionGestureTarget> gestureTarget;

* In `prepareForSegue` in your master view controller tell the transition which cell (view) originated the transition and, optionally, set the gesture target on the detail view controller (if you want to uyse the interactive 'back' gestures):

        // the transition controller needs to know the view (cell)
        // that originated the segue in order to be able to "split"
        // the table view correctly
        self.zoomTransition.sourceView = [self.tableView cellForRowAtIndexPath:indexPath];

        // pass the custom transition to the destination controller
        // so it can use it when setting up its gesture recognizers
        [[segue destinationViewController] setGestureTarget:self.zoomTransition];

* If you want the interactive 'back' gestures, in `viewDidLoad` in your detail view controller setup the gesture recognizers:

        // setup a pinch gesture recognizer and make the target the custom transition handler
        UIPinchGestureRecognizer *pinchRecognizer = [[UIPinchGestureRecognizer alloc] initWithTarget:self.gestureTarget action:@selector(handlePinch:)];
        [self.view addGestureRecognizer:pinchRecognizer];
    
        // setup an edge pan gesture recognizer and make the target the custom transition handler
        UIScreenEdgePanGestureRecognizer *edgePanRecognizer = [[UIScreenEdgePanGestureRecognizer alloc] initWithTarget:self.gestureTarget action:@selector(handleEdgePan:)];
        edgePanRecognizer.edges = UIRectEdgeLeft;
        [self.view addGestureRecognizer:edgePanRecognizer];

* That's it!

## License
Copyright © 2013 Michael Brown (me@michael-brown.net)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

    