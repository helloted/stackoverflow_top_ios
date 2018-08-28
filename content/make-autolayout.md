# 使用自动布局？
___



> 1

```objective-c
    customView.translatesAutoresizingMaskIntoConstraints = NO;
    NSLayoutConstraint *topConstraint =
    [NSLayoutConstraint constraintWithItem:customView
                                 attribute:NSLayoutAttributeTop
                                 relatedBy:NSLayoutRelationEqual
                                    toItem:self.view
                                 attribute:NSLayoutAttributeTop
                                multiplier:1.f
                                  constant:0.f];
    
    NSLayoutConstraint *rightConstraint =
    [NSLayoutConstraint constraintWithItem:customView
                                 attribute:NSLayoutAttributeRight
                                 relatedBy:NSLayoutRelationEqual
                                    toItem:self.view
                                 attribute:NSLayoutAttributeRight
                                multiplier:1.f
                                  constant:0.f];

    NSLayoutConstraint *leftConstraint =
    [NSLayoutConstraint constraintWithItem:customView
                                 attribute:NSLayoutAttributeLeft
                                 relatedBy:NSLayoutRelationEqual
                                    toItem:self.view
                                 attribute:NSLayoutAttributeLeft
                                multiplier:1.f
                                  constant:0.f];

    NSLayoutConstraint *bottomConstraint =
    [NSLayoutConstraint constraintWithItem:customView
                                 attribute:NSLayoutAttributeBottom
                                 relatedBy:NSLayoutRelationEqual
                                    toItem:self.view
                                 attribute:NSLayoutAttributeBottom
                                multiplier:1.f
                                  constant:0.f];
    
    [self.view addConstraint:topConstraint];
    [self.view addConstraint:rightConstraint];
    [self.view addConstraint:leftConstraint];
    [self.view addConstraint:bottomConstraint];

```