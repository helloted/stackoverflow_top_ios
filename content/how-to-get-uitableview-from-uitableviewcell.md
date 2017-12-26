# 获取UITableViewCell的UITableView
[How to get UITableView from UITableViewCell?](https://stackoverflow.com/questions/15711645/how-to-get-uitableview-from-uitableviewcell)

___



> 1

```objc
id view = [tableViewCellInstance superview];

while (view && [view isKindOfClass:[UITableView class]] == NO) {
    view = [view superview]; 
}

UITableView *tableView = (UITableView *)view;
```
> 2

```objc
@interface SOUITableViewCell

@property (weak, nonatomic) UITableView *tableView;

@end
```

注意是弱引用，否则会导致循环引用