# 如何在NSUserDefaults里保存一个自定义对象？
[How to store custom objects in NSUserDefaults](https://stackoverflow.com/questions/2315948/how-to-store-custom-objects-in-nsuserdefaults)

___



> 1

你需要实现NSCopying协议并实现以下方法

```objc
- (void)encodeWithCoder:(NSCoder *)encoder {
    //Encode properties, other class variables, etc
    [encoder encodeObject:self.question forKey:@"question"];
    [encoder encodeObject:self.categoryName forKey:@"category"];
    [encoder encodeObject:self.subCategoryName forKey:@"subcategory"];
}

- (id)initWithCoder:(NSCoder *)decoder {
    if((self = [super init])) {
        //decode properties, other class vars
        self.question = [decoder decodeObjectForKey:@"question"];
        self.categoryName = [decoder decodeObjectForKey:@"category"];
        self.subCategoryName = [decoder decodeObjectForKey:@"subcategory"];
    }
    return self;
}
```

在`NSUserDefaults`读写:

```objc
- (void)saveCustomObject:(MyObject *)object key:(NSString *)key {
    NSData *encodedObject = [NSKeyedArchiver archivedDataWithRootObject:object];
    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
    [defaults setObject:encodedObject forKey:key];
    [defaults synchronize];

}

- (MyObject *)loadCustomObjectWithKey:(NSString *)key {
    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
    NSData *encodedObject = [defaults objectForKey:key];
    MyObject *object = [NSKeyedUnarchiver unarchiveObjectWithData:encodedObject];
    return object;
}
```