## FCOverlay

FCOverlay allows you to present a new view controller hierarchy in a new window. 

When you present a view controller via one of the provided methods it is presented in
a new window on top of all existing windows (including those previously generated by 
FCOverlay). The new window is transparent so you can use this to create HUD's, 
alerts etc... (run the example project to get some inspiration).

The nice thing about FCOverlay is that you don't have to keep track of the current visible
view controller and present a new view controller on that view controller. You can just
present and dismiss any kind of view controller on top of all others from everywhere in 
your code.

FCOverlay allows you to present this to the user as if it is just a "normal" controller
transition. The example code shows how to use iOS 7 custom transitions, present on
different window levels (above or below the status bar), and to present alert type
view controllers. 

### Usage

You can use the FCOverlay presentOverlayWithViewController class methods to immediately 
present a view controller (with custom transitioning if you like).

    ExampleViewController *exampleController = [[ExampleViewController alloc] init];
    
    exampleController.transitioningDelegate = self.transitioningDelegate;
    
    [FCOverlay presentOverlayWithViewController:exampleController
                                    windowLevel:UIWindowLevelNormal
                                       animated:YES
                                     completion:nil];
                                     
If you want to present view controllers one at a time you can also use the 
queueOverlayWithViewController class methods.

    AlertViewController *alertController = [[AlertViewController alloc] init];
    
    alertController.alertTitleString = @"This is the first queued alert";
    alertController.alertMessageString = @"After this alert will follow a new alert, alertception style!";
    alertController.modalTransitionStyle = UIModalTransitionStyleCrossDissolve;
    
     // queue the first alert (this will be presented immediately)
    [FCOverlay queueOverlayWithViewController:alertController
                                  windowLevel:UIWindowLevelAlert
                                     animated:NO
                                   completion:nil];
    
    // queue the second alert
    alertController = [[AlertViewController alloc] init];
    
    alertController.alertTitleString = @"This is the second queued alert";
    alertController.alertMessageString = @"After this alert there will be no more alerts in the queue!";
    alertController.modalTransitionStyle = UIModalTransitionStyleCrossDissolve;
    
    [FCOverlay queueOverlayWithViewController:alertController
                                  windowLevel:UIWindowLevelAlert
                                     animated:NO
                                   completion:nil];
                                     


