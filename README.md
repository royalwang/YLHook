[Aspects](https://github.com/steipete/Aspects) is a delightful, simple library for aspect oriented programming.

YLHook enables [Aspects](https://github.com/steipete/Aspects) to support functional programming.



## Why to use YLHook

We often print logs or statistics everywhere. AOP provides a concise way to solve those [Cross-cutting Concerns](https://en.wikipedia.org/wiki/Cross-cutting_concern).

Aspects Demo:

```objc
[UIViewController aspect_hookSelector:@selector(viewWillAppear:) withOptions:AspectPositionAfter usingBlock:^(id<AspectInfo> aspectInfo, BOOL animated) {
    NSLog(@"[%@]before viewWillAppear",[[aspectInfo instance] class]);
} error:NULL];
```

It's really very simple. But it's not clean when we need hook a lot of methods at one class.

It will be like this:

```objc
[UIViewController aspect_hookSelector:@selector(viewWillAppear:) withOptions:AspectPositionAfter usingBlock:^(id<AspectInfo> aspectInfo, BOOL animated) {
    NSLog(@"[%@]before viewWillAppear",[[aspectInfo instance] class]);
} error:NULL];

[UIViewController aspect_hookSelector:@selector(viewDidLoad:) withOptions:AspectPositionAfter usingBlock:^(id<AspectInfo> aspectInfo, BOOL animated) {
    NSLog(@"[%@]before viewDidLoad",[[aspectInfo instance] class]);
} error:NULL];

[UIViewController aspect_hookSelector:@selector(viewDidAppear:) withOptions:AspectPositionAfter usingBlock:^(id<AspectInfo> aspectInfo, BOOL animated) {
    NSLog(@"[%@]before viewDidAppear",[[aspectInfo instance] class]);
} error:NULL];
```



Now, you can hook by this way:

```objc
[[YLHook hookClassByName:@"UIViewController"] makeEvents:^(YLEventMaker *make) {
        make.after.selector(@"viewDidLoad").block(^(id<AspectInfo> aspectInfo){
            NSLog(@"[%@]after viewDidLoad",[[aspectInfo instance] class]);
        });
        make.before.selector(@"viewWillAppear:").block(^(id<AspectInfo> aspectInfo){
            NSLog(@"[%@]before viewWillAppear",[[aspectInfo instance] class]);
        });
        make.before.selector(@"viewDidAppear:").block(^(id<AspectInfo> aspectInfo){
            NSLog(@"[%@]before viewDidAppear",[[aspectInfo instance] class]);
        });
    }];
```

This style is like [Masonry](https://github.com/SnapKit/Masonry). In fact, I did refer to Masonry's realization. 



## Installation

You can install by [Cocopods](https://github.com/CocoaPods/CocoaPods) soon.



## License

YLHook is released under the MIT license. See [LICENSE](./LICENSE) for details.