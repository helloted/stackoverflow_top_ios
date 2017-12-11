# application几种状态
[applicationWillEnterForeground vs. applicationDidBecomeActive, applicationWillResignActive vs. applicationDidEnterBackground](https://stackoverflow.com/questions/3712979/applicationwillenterforeground-vs-applicationdidbecomeactive-applicationwillre)

___



> 1

**applicationWillEnterForeground:** 会被调用当app被重新启动 (不管是通过springboard, app切换或者URL)，在APP被放入后台后，这个方法只会被执行一次，但是 **applicationDidBecomeActive:** APP启动后可能被执行很多次. 这就让 **applicationWillEnterForeground:** 成为理想的配置，针对某些重新启动后只会发生一次的事件.

**applicationWillEnterForeground::**

- APP被重新启动(不管是通过springboard, app切换或者URL)
- 在 **applicationDidBecomeActive:**之前

**applicationDidBecomeActive:**

- app第一次启动并且在 `application:didFinishLaunchingWithOptions:`之后
- 在 **applicationWillEnterForeground:** 如果没有 URL 需要去处理.
- 在 `application:handleOpenURL:` 被调用之后.
- 在 **applicationWillResignActive:** 之后:如果用户忽略电话或者短信.

**applicationWillResignActive: is called:**

- 当有打断比如电话进来.
  - 如果用户接电话会调用 **applicationDidEnterBackground:** 会被调用.
  - 如果用户忽略这个电话 **applicationDidBecomeActive:** 会被调用.
- 当按了 home按键或者用户切换apps.
- 文档说，你应该
  - 暂停在执行的任务
  - timers取消
  - 暂停游戏
  - 减小 OpenGL frame rates

**applicationDidEnterBackground: is called:**

- 在 **applicationWillResignActive:**之后
- 文档说你应该
  - 释放共享资源
  - 保存用户数据
  - 取消timers
  - 保存app状态以便于你重建如果app被终止的话.
  - 不更新UI
- 你有 5s的时间来处理事件直到方法返回
  - 如果你没有返回-app在5s内被终止
  - 你可以申请更多的时间通过调用 `beginBackgroundTaskWithExpirationHandler:`