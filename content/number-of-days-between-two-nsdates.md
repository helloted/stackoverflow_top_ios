# 计算两个NSDate之间的天数？
[Number of days between two NSDates](https://stackoverflow.com/questions/4739483/number-of-days-between-two-nsdates)

___



> 1

#### Objective-C:

```objc
+ (NSInteger)daysBetweenDate:(NSDate*)fromDateTime andDate:(NSDate*)toDateTime
{
    NSDate *fromDate;
    NSDate *toDate;

    NSCalendar *calendar = [NSCalendar currentCalendar];

    [calendar rangeOfUnit:NSCalendarUnitDay startDate:&fromDate
        interval:NULL forDate:fromDateTime];
    [calendar rangeOfUnit:NSCalendarUnitDay startDate:&toDate
        interval:NULL forDate:toDateTime];

    NSDateComponents *difference = [calendar components:NSCalendarUnitDay
        fromDate:fromDate toDate:toDate options:0];

    return [difference day];
}
```

#### Swift:

```swift
extension NSDate {
  func numberOfDaysUntilDateTime(toDateTime: NSDate, inTimeZone timeZone: NSTimeZone? = nil) -> Int {
    let calendar = NSCalendar.currentCalendar()
    if let timeZone = timeZone {
      calendar.timeZone = timeZone
    }

    var fromDate: NSDate?, toDate: NSDate?

    calendar.rangeOfUnit(.Day, startDate: &fromDate, interval: nil, forDate: self)
    calendar.rangeOfUnit(.Day, startDate: &toDate, interval: nil, forDate: toDateTime)

    let difference = calendar.components(.Day, fromDate: fromDate!, toDate: toDate!, options: [])
    return difference.day
  }
}
```

