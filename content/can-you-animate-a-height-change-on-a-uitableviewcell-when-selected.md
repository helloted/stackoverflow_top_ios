# 选中UITableViewCell时动画更改高度
[Can you animate a height change on a UITableViewCell when selected?](https://stackoverflow.com/questions/460014/can-you-animate-a-height-change-on-a-uitableviewcell-when-selected)

___



> 1

我找到了一个简单的方法来解决这个问题

将cell的高度存在 `tableView: heightForRowAtIndexPath:`, 当你想要动画地更改高度,简单地调用这个方法：

```objc
[tableView beginUpdates];
[tableView endUpdates];
```

你会发现你不需要reload，但是 `UITableView` 知道去重画cells, 就能动画地更改cell高度

```objc
- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath {
// Deselect cell
[tableView deselectRowAtIndexPath:indexPath animated:TRUE];

// Toggle 'selected' state
BOOL isSelected = ![self cellIsSelected:indexPath];

// Store cell 'selected' state keyed on indexPath
NSNumber *selectedIndex = [NSNumber numberWithBool:isSelected];
[selectedIndexes setObject:selectedIndex forKey:indexPath];

// This is where magic happens...
[demoTableView beginUpdates];
[demoTableView endUpdates];
}
```

