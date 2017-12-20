# 创建一个Selectors的数组
[how to create an “array of selectors”](https://stackoverflow.com/questions/2226520/how-to-create-an-array-of-selectors)

___



> 1

使用C数组

```c
static const SEL selectors[] = {@selector(method1),
                                ....
                                @selector(method7)};

...

for (int i = 0; i < sizeof(selectors)/sizeof(selectors[0]); i++) {
  [self performSelector:selectors[i]];
  // ....
}
```

> 2

存储selector的指针

```
[NSValue valueWithPointer:@selector(x)]
```

```
SEL x = (SEL)selectorValue.pointerValue;
```

