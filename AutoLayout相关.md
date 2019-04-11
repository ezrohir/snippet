# 播放器MGPlayerCommonBottomView

[toc]

### 一、功能描述
在点播回看状态下，能控制播放器的时移；在直播状态下，能控制后拖的时移，前拖大于当前播放时间的，只能到当前播放时间。
#### 进度条
在类中的属性：
```
@property (nonatomic, strong) WCSlider *slider;
```
在类中的事件：
```
#pragma mark -- Slider Actions

- (void)videoSliderValueBeganChange:(WCSlider *)sender {
    //开始拖动
}

- (void)videoSlierChangeValue:(WCSlider *)sender {
    //value变化
}

- (void)videoSlierChangeValueEnd:(WCSlider *)sender {
    //拖动结束
}

```

#### 开始时间
显示格式 00:00
在类中的属性：
```
@property (nonatomic, strong) UILabel *portraitLeftTimeLbl;
```

#### 结束时间
显示格式 00:00
在类中的属性：
```
@property (nonatomic, strong) UILabel *portraitRightTimeLbl;
```

#### 横屏时间
显示格式 00:00/00:00:00
在类中的属性：
```
@property (nonatomic, strong) UILabel *landSpaceTimeLbl;
```

#### 全屏按钮
横竖屏切换按钮
在类中的属性：
```
@property (nonatomic, strong) UILabel *playerStateBtn;
```
响应事件抛出
```
[self.playerStateButton blockClick:^{
    [weakSelf routerEvent:WCPlayerBottom_PlayerStateKey info:weakSelf.playerStateButton];
}];
```


#### 开始、暂停按钮
在类中的属性：
```
@property (nonatomic, strong) UIButton *playBtn;
```
响应事件抛出
```
[self.playButton blockClick:^{
        [weakSelf routerEvent:WCPlayerBottom_PlayKey info:@(weakSelf.playState)];
    }];
```

#### 下一集按钮
在类中的属性：
```
@property (nonatomic, strong) UIButton *nextButton;
```
响应事件抛出
```
[self.nextButton blockClick:^{
        [weakSelf routerEvent:kMGPlayerNextEpisodeEventName info:nil];
    }];
```


#### 清晰度按钮
在类中的属性：
```
@property (nonatomic, strong) UIButton *clarityBtn;
```
响应事件抛出
```
[self.clarityBtn blockClick:^{
    [weak_self routerEvent:WCPlayerTop_SharpnessKey info:weak_self.clarityButton];
}];
```

#### 节目单按钮
在类中的属性：
```
@property (nonatomic, strong) UIButton *programBtn;
```
响应事件抛出
```
[self.programBtn blockClick:^{
    [weakSelf routerEvent:MGMediaProgramListShowEvent info:nil];
}];
```

#### 红包按钮
在类中的属性：
```
@property (nonatomic, strong) MGPlayerWatchMissionButton *missionBtn;
```
响应事件抛出
```
[self.missionBtn blockClick:^{
    [weakSelf routerEvent:WCPlayerWatchMissionEventName info:nil];
}];
```

#### 换台按钮
在类中的属性：
```
@property (nonatomic, strong) UIButton *changeChannelBtn;
```
响应事件抛出
```
[self.changeChannelBtn blockClick:^{
    [weak_self routerEvent:MGMediaChangeChannelShowEvent info:nil];
}];
```

#### 选集按钮

#### 多路解说按钮

#### 小窗播放按钮
在类中的属性:
```
@property (nonatomic, strong) UIButton *switchToWindowBtn;  
```
#### 赛事数据按钮
在类中的属性：
```
@property (nonatomic, strong) UIButton *matchDataBtn;
```

#### 播放倍数按钮
在类中的属性：
```
@property (nonatomic, strong) UIButton *playRateBtn;
```



### 二、bottomView状态
#### 竖屏
该状态下只有[开始时间](开始时间)、结束时间、进度条、全屏按钮和暂停/开始按钮。
#### 横屏
该状态下根据播放器类型 [MGPlayerCommonBottomViewType](MGPlayerCommonBottomViewType类型) UI元素有差异

### 三、MGPlayerCommonBottomViewType 播放器类型类型
改类型为枚举结构
```

typedef NS_ENUM(NSInteger, MGPlayerCommonBottomViewType) {
    MGPlayerCommonBottomViewTypeDetault,                // 最小元素
    MGPlayerCommonBottomViewTypeVOD,                    // 点播
    MGPlayerCommonBottomViewTypeLiving,                 // 直播
    MGPlayerCommonBottomViewTypePendant,                // 挂件
} NS_ENUM_AVAILABLE_IOS(8_0);

```
只有横屏状态下类型显示的样式才不一样, 类型显示如下.

#### 点播横屏
点播下只有暂停/开始按钮,横屏时间,清晰度按钮,红包按钮.

#### 开路直播
直播下只有暂停/开始按钮,横屏时间,清晰度按钮,换台按钮,节目单按钮,红包按钮.

#### 挂件
点播下只有暂停/开始按钮,横屏时间,清晰度按钮,红包按钮.


### 四、状态监听
监听的App事件有:
+ kMGMLSwitching  清晰度切换中
+ kClaritySwitchCompleted  清晰度切换完成

系统事件有:
UIApplicationWillChangeStatusBarOrientationNotification

### 五、布局方法
根据UI元素集合units显示与隐藏UI
```
- (void)updateUIElementVisibilityWithUnits:(MGPlayerBottomViewUnits)unit;
```
横屏布局
```
- (void)updateLandSpaceConstraintsWithUnits:(MGPlayerBottomViewUnits)unit;
```
竖屏布局
```
- (void)updateLandSpaceConstraintsWithUnits:(MGPlayerBottomViewUnits)unit;
```


### 六、初始化方法
```
- (instancetype)initWithViewModel:(MGPlayerCommonBottomViewModel *)viewModel;
```
### 七、public方法
