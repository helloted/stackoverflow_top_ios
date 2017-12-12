# @try - catch block
[@try - catch block in Objective-c](https://stackoverflow.com/questions/3363612/try-catch-block-in-objective-c)

___



> 1

```objc
NSString *test = @"test";
    unichar a;
    int index = 5;

    @try {
        a = [test characterAtIndex:index];
    }
    @catch (NSException *exception) {
        NSLog(@"%@", exception.reason);
    }
    @finally {
        NSLog(@"Char at index %d cannot be found", index);
        NSLog(@"Max index is: %d", [test length]-1);
    }
```

Log:

> [__NSCFConstantString characterAtIndex:]: Range or index out of bounds
>
> Char at index 5 cannot be found
>
> Max index is: 3