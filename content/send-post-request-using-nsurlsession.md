# 用NSURLSession发送一个POST请求
[Send POST request using NSURLSession](https://stackoverflow.com/questions/19099448/send-post-request-using-nsurlsession)

___



> 1

你可以用NSDictionary包装一下参数，下面的代码可以发送这些参数到一个JSON Server

```objc
NSError *error;

NSURLSessionConfiguration *configuration = [NSURLSessionConfiguration defaultSessionConfiguration];
NSURLSession *session = [NSURLSession sessionWithConfiguration:configuration delegate:self delegateQueue:nil];
NSURL *url = [NSURL URLWithString:@"[JSON SERVER"];
NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url
                                                       cachePolicy:NSURLRequestUseProtocolCachePolicy
                                                   timeoutInterval:60.0];

[request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
[request addValue:@"application/json" forHTTPHeaderField:@"Accept"];

[request setHTTPMethod:@"POST"];
NSDictionary *mapData = [[NSDictionary alloc] initWithObjectsAndKeys: @"TEST IOS", @"name",
                     @"IOS TYPE", @"typemap",
                     nil];
NSData *postData = [NSJSONSerialization dataWithJSONObject:mapData options:0 error:&error];
[request setHTTPBody:postData];


NSURLSessionDataTask *postDataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {

}];

[postDataTask resume];
```