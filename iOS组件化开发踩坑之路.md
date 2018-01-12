## iOS组件化开发踩坑之路

* 当前组件工程如果需要继承某个被当前组件依赖组件中的类，在 `#import "类名称.h"` 时，会报错。应该使用 `#import <组件名称/类名称.h>`

* 当前组件有警告时，`pod lib lint` / `pod spec lint` / `pod repo push` 都会失败。应在上述命令后追加 `--allow-warnings`

* 当前组件依赖的组件或者间接依赖的组件为私有时，需要在 podfile 文件最上方添加 `source '被依赖或者被间接依赖组件的pods地址1'`
`source '被依赖或者被间接依赖组件的pods地址2'`，向上依赖的所有组件的 pods 地址都要加上，无论向上依赖的组件是否私有

* 私有组件不需要 `pod spec lint`、`pod trunk push`

* 组件中 A 中有两个 subspec，a1 和 a2。当 a1 被 a2 依赖时，应使用 s2.dependency 'A/a1' 设置依赖

* 组件a中依赖组件b，当组件a中某个类a_c需要在.h文件中引用组件b中的某个类b_c,应该使用@class 而不能使用#import,否则pod lib lint报错

* `pod install` 不到最新版本，应使用 `pod update`； `pod update` 不到最新版本在 podfile 文件中追加 `, :git=>'仓库地址'`

* pod lib lint 不到最新版本应该早 podspec 文件中追加 `,'~> 版本号'`

* pod update 不到组件 cmp_a 最新版本是因为当前需要 pod 的组件 cmp_b 同样依赖了 cmp_a，但是 cmp_b 中依赖 cmp_a 的时候没有在 cmp_b 的 podspec 文件中显示依赖（依赖具体的版本号，'~> x.x.x'） cmp_a 的最新版本。cmp_b 中如果不显示依赖版本号的话可能对后续 pod 造成影响。

* 遇到 “...required by `Podfile.lock`” 报错，删除 Podfile.lock 文件,然后再 `pod install`

* 当前 pods 有更新，使用 `pod update`；跨 pods 更新，使用 `pod repo update`。

* 当 `pod install/pod update` 时，提示“Specs satisfying the `JQR_Route, JQR_Route (~> 0.2.17)` dependency were found, but they required a higher minimum deployment target.”，需要执行 `pod repo update` 更新一下。