## Cocoapods 打静态库碰到的问题

#### podspec 语法问题
```
  s.vendored_frameworks = "GoogleAdModule/Frameworks/GoogleMobileAds.framework"
```
路径以 .podspec 所在目录为跟目录,相对路径

#### 使用私有库无法找到索引信息问题
```
  pod install
  报 Unable to find a spectionfication for 'YourPodModule'
```
需要在 Podfile 告诉 pod 在哪个源哪去拉去 specs 仓库信息.


#### 校验问题
对于 spec 包含了三方静态库, 需使用 --use-libraries 后缀.     
对于忽略 warning 可使用 --allow-warnings , 具体参考 pod spec lint --help

#### 打包库问题
```
  pod package GameADModule.podspec --no-mangle --force
```
对于包含静态库 需要使用 --no-mangle

#### 打包设置额外条件
```
    pod package GameADModule.podspec --no-mangle --force
    #error The Google Mobile Ads SDK doesn't support linking with armv7s. Remove armv7s from "ARCHS" (Architectures) in your Build Settings.
```
理论上 podspec 有字段支持额外参数, 得研究.


[干货博客,覆盖了我所有碰到的问题](http://www.devzhang.cn/2018/02/01/Cocoapods二进制化方案/)
