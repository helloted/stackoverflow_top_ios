# UITableView填满分割线
[How to set the full width of separator in UITableView](https://stackoverflow.com/questions/26519248/how-to-set-the-full-width-of-separator-in-uitableview)

___



> 1

#### Swift:

```swift
cell.preservesSuperviewLayoutMargins = false
cell.separatorInset = UIEdgeInsets.zero
cell.layoutMargins = UIEdgeInsets.zero
```

#### Objective-C:

```objc
-(void)tableView:(UITableView *)tableView willDisplayCell:(UITableViewCell *)cell forRowAtIndexPath:(NSIndexPath *)indexPath
{
    if ([cell respondsToSelector:@selector(setSeparatorInset:)]) {
        [cell setSeparatorInset:UIEdgeInsetsZero];
    }

    if ([cell respondsToSelector:@selector(setLayoutMargins:)]) {
        [cell setLayoutMargins:UIEdgeInsetsZero];
    }
}

-(void)viewDidLayoutSubviews
{
    [super viewDidLayoutSubviews];
    if ([self.tableView respondsToSelector:@selector(setSeparatorInset:)]) {
        [self.tableView setSeparatorInset:UIEdgeInsetsZero];
    }

    if ([self.tableView respondsToSelector:@selector(setLayoutMargins:)]) {
        [self.tableView setLayoutMargins:UIEdgeInsetsZero];
    }
}
```