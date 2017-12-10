# UITableViewCell，如何滑动删除？
[UITableViewCell, show delete button on swipe](https://stackoverflow.com/questions/3309484/uitableviewcell-show-delete-button-on-swipe)

___



> 1

```
// During startup (-viewDidLoad or in storyboard) do:
self.tableView.allowsMultipleSelectionDuringEditing = NO;


// Override to support conditional editing of the table view.
// This only needs to be implemented if you are going to be returning NO
// for some items. By default, all items are editable.
- (BOOL)tableView:(UITableView *)tableView canEditRowAtIndexPath:(NSIndexPath *)indexPath {
    // Return YES if you want the specified item to be editable.
    return YES;
}

// Override to support editing the table view.
- (void)tableView:(UITableView *)tableView commitEditingStyle:(UITableViewCellEditingStyle)editingStyle forRowAtIndexPath:(NSIndexPath *)indexPath {
    if (editingStyle == UITableViewCellEditingStyleDelete) {
        //add code here for when you hit delete
    }    
}
```