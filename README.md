# WHToast

WHToast是一个轻量级的提示控件，没有任何依赖。先来看一下效果图。

![whtoast.gif](https://upload-images.jianshu.io/upload_images/3873004-50507445e23bb9f2.gif?imageMogr2/auto-orient/strip)

使用方法也非常简单，下面是使用步骤。

### 1. 可以直接在本页面下载文件拖入WHToast文件到工程，也可以使用pod。

> 如果pod找不到WHToast，先执行 pod setup

```objc
pod 'WHToast'

// 如果pod找不到WHToast，先执行 pod setup
pod setup
```

### 2. 导图WHToast.h头文件

```objc
// pod
#import <WHToast.h>
// 直接拖入文件
#import "WHToast.h"
```

### 3. 说明

> 每种显示类型都有两个方法，第一个方法默认显示在屏幕中间，第二个方法带有originY参数的是可以自定义显示位置，也就是自定义frame.origin.y。（注意：如果传入的originY<=0，也是显示在屏幕中间）。

### 4. 显示文字提示。

```objc
// 显示在页面中间，dismissDelay代表多久之后消失
[WHToast showMessage:@"测试一下" dismissDelay:2 finishHandler:^{
  NSLog(@"省略n行代码");
}];

// 自定义frame.origin.y
[WHToast showMessage:@"测试一下" originY:200 dismissDelay:2 finishHandler:^{
  NSLog(@"省略n行代码");
}];
```

### 5. 显示带有成功图标的提示。

```objc
// 显示在页面中间，dismissDelay代表多久之后消失
[WHToast showSuccessWithMessage:@"测试一下" dismissDelay:2 finishHandler:^{
  NSLog(@"省略n行代码");
}];

// 自定义frame.origin.y
[WHToast showSuccessWithMessage:@"测试一下" originY:100 dismissDelay:2 finishHandler:^{
  NSLog(@"省略n行代码");
}];
```

### 6. 带有错误图标的提示。

```objc
// 显示在页面中间，dismissDelay代表多久之后消失
[WHToast showErrorWithMessage:@"测试一下" dismissDelay:2 finishHandler:^{
  NSLog(@"省略n行代码");
}];

// 自定义frame.origin.y
[WHToast showErrorWithMessage:@"测试一下" originY:200 dismissDelay:2 finishHandler:^{
  NSLog(@"省略n行代码");
}];
```

### 7. 传入一个图片，自定义图标提示。

```objc
// 显示自定义图片，如果message传入nil，则只显示图片，dismissDelay代表多久之后消失
[WHToast showImage:[UIImage imageNamed:@"123"] message:nil dismissDelay:2 finishHandler:^{
  NSLog(@"省略n行代码");
}];

// 自定义frame.origin.y，显示自定义图片
[WHToast showImage:[UIImage imageNamed:@"123"] message:@"测试一下" originY:200 dismissDelay:2 finishHandler:^{
  NSLog(@"省略n行代码");
}];
```

### 8. 全局自定义显示样式。

>直接使用WHToast的类方法就可以做全局自定义设置。样式如下。

```objc 

/** 是否有背景遮罩，默认有 */
+ (void)setShowMask:(BOOL)showMask;

/** 遮罩颜色，默认透明 */
+ (void)setMaskColor:(UIColor *)maskColor;

/** 遮罩是否遮住导航栏，默认遮住 */
+ (void)setMaskCoverNav:(BOOL)maskCoverNav;

/** 边距，默认12 */
+ (void)setPadding:(CGFloat)padding;

/** 提示图片尺寸，默认（30,30）*/
+ (void)setTipImageSize:(CGSize)tipImageSize;

/** 圆角，默认7 */
+ (void)setCornerRadius:(CGFloat)cornerRadius;

/** 背景颜色，默认[UIColor colorWithWhite:0 alpha:0.8] */
+ (void)setBackColor:(UIColor *)backColor;

/** 成功/失败 图标颜色，默认白色 */
+ (void)setIconColor:(UIColor *)iconColor;

/** 文字颜色，默认白色 */
+ (void)setTextColor:(UIColor *)textColor;

/** 文字大小，默认15 */
+ (void)setFontSize:(CGFloat)fontSize;

/** 恢复默认配置 */
+ (void)resetConfig;

// 调用方式
[WHToast setShowMask:NO];
[WHToast setMaskColor:[UIColor colorWithWhite:0 alpha:0.6]];
[WHToast setMaskCoverNav:NO];
[WHToast setTipImageSize:CGSizeMake(50, 50)];
[WHToast setFontSize:30];
[WHToast setPadding:20];
[WHToast setCornerRadius:20];
[WHToast setIconColor:[UIColor blackColor]];
[WHToast setBackColor:[UIColor whiteColor]];
[WHToast setTextColor:[UIColor blackColor]];

```

### 9. 下面贴出来所有方法。

```objc
/** 仅文字，展示在屏幕中间 */
+ (void)showMessage:(NSString *)message dismissDelay:(NSTimeInterval)delay finishHandler:(dispatch_block_t)handler;

/** 仅文字，自定义frame.origin.y 如果（originY <= 0）会展示在屏幕中间 */
+ (void)showMessage:(NSString *)message originY:(CGFloat)originY dismissDelay:(NSTimeInterval)delay finishHandler:(dispatch_block_t)handler;

/** 成功图标和文字，展示在屏幕中间 */
+ (void)showSuccessWithMessage:(NSString *)message dismissDelay:(NSTimeInterval)delay finishHandler:(dispatch_block_t)handler;

/** 成功图标和文字，自定义frame.origin.y 如果（originY <= 0）会展示在屏幕中间 */
+ (void)showSuccessWithMessage:(NSString *)message originY:(CGFloat)originY dismissDelay:(NSTimeInterval)delay finishHandler:(dispatch_block_t)handler;

/** 失败图标和文字，展示在屏幕中间 */
+ (void)showErrorWithMessage:(NSString *)message dismissDelay:(NSTimeInterval)delay finishHandler:(dispatch_block_t)handler;

/** 失败图标和文字，自定义frame.origin.y 如果（originY <= 0）会展示在屏幕中间 */
+ (void)showErrorWithMessage:(NSString *)message originY:(CGFloat)originY dismissDelay:(NSTimeInterval)delay finishHandler:(dispatch_block_t)handler;

/** 自定义图片和文字，展示在屏幕中间。 如果message传入nil，则只显示图片 */
+ (void)showImage:(UIImage *)image message:(NSString *)message dismissDelay:(NSTimeInterval)delay finishHandler:(dispatch_block_t)handler;

/** 自定义图片和文字，自定义frame.origin.y 如果（originY <= 0）会展示在屏幕中间。如果message传入nil，则只显示图片 */
+ (void)showImage:(UIImage *)image message:(NSString *)message originY:(CGFloat)originY dismissDelay:(NSTimeInterval)delay finishHandler:(dispatch_block_t)handler;

/** 主动消失 */
+ (void)hide;


/******************************************************/
/******************  设置全局样式  **********************/
/******************************************************/

/** 是否有背景遮罩，默认有 */
+ (void)setShowMask:(BOOL)showMask;

/** 遮罩颜色，默认透明 */
+ (void)setMaskColor:(UIColor *)maskColor;

/** 遮罩是否遮住导航栏，默认遮住 */
+ (void)setMaskCoverNav:(BOOL)maskCoverNav;

/** 边距，默认12 */
+ (void)setPadding:(CGFloat)padding;

/** 提示图片尺寸，默认（30,30）*/
+ (void)setTipImageSize:(CGSize)tipImageSize;

/** 圆角，默认7 */
+ (void)setCornerRadius:(CGFloat)cornerRadius;

/** 背景颜色，默认[UIColor colorWithWhite:0 alpha:0.8] */
+ (void)setBackColor:(UIColor *)backColor;

/** 成功/失败 图标颜色，默认白色 */
+ (void)setIconColor:(UIColor *)iconColor;

/** 文字颜色，默认白色 */
+ (void)setTextColor:(UIColor *)textColor;

/** 文字大小，默认15 */
+ (void)setFontSize:(CGFloat)fontSize;

/** 恢复默认配置 */
+ (void)resetConfig;

```
