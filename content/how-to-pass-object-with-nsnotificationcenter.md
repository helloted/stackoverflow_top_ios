# NSNotificationCenter传递对象
[How to pass object with NSNotificationCenter](https://stackoverflow.com/questions/7896646/how-to-pass-object-with-nsnotificationcenter)

___



> 1

你可以通过userInfo变量来传递信息，信息包裹在字典里：

**Class A (发送者):**

```
YourDataObject *message = [[YourDataObject alloc] init];
// set your message properties
NSDictionary *dict = [NSDictionary dictionaryWithObject:message forKey:@"message"];
[[NSNotificationCenter defaultCenter] postNotificationName:@"NotificationMessageEvent" object:nil userInfo:dict];
```

**Class B (接受者):**

```
- (void)viewDidLoad
{
    [super viewDidLoad];
    [[NSNotificationCenter defaultCenter]
     addObserver:self selector:@selector(triggerAction:) name:@"NotificationMessageEvent" object:nil];
}

#pragma mark - Notification
-(void) triggerAction:(NSNotification *) notification
{
    NSDictionary *dict = notification.userInfo;
    YourDataObject *message = [dict valueForKey:@"message"];
    if (message != nil) {
        // do stuff here with your message data
    }
}
```

