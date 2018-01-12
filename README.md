# LJAvatarBrowserDemo
一款简单易用,轻量级图片查看工具

![效果图](https://github.com/iBoCoding/LJAvatarBrowser/blob/master/result.gif)

## <a id="How_to_use_LJAvatarBrowser"></a>How to use LJAvatarBrowser
* Installation with CocoaPods：`pod 'LJAvatarBrowser'`
* Manual import：
    * Drag All files in the `LJAvatarBrowser` folder to project
    * Import the main file：`#import "LJAvatarBrowser.h"
    
## <a id="Example"></a>Example

```swift
[LJAvatarBrowser showImageView:imageView];

Or

[LJAvatarBrowser showImageView:imageView originUrl:url];

Or

[LJAvatarBrowser showPreviewPhotos:[_imgArray mutableCopy] delegate:self containerView:containerView previewIndex:tag placeholderImage:nil]
```

## <a id="LJAvatarBrowser.h"></a>LJAvatarBrowser.h

```swift
import <Foundation/Foundation.h>

@class LJAvatarBrowser;

@protocol LJAvatarBrowserDelegate<NSObject>

@optional

/**
 返回一个高清的url
 @param browser LJAvatarBrowser
 @param index 滚动下标
 @return urlString
 */
- (NSString *)photoBrowser:(LJAvatarBrowser *)browser originImageURLForIndex:(NSInteger)index;

/**
 返回占位图
 @param browser LJAvatarBrowser
 @param index 滚动下标
 @return placeholderImage
 */
- (UIImage *)photoBrowser:(LJAvatarBrowser *)browser placeholderImageForIndex:(NSInteger)index;
/**
 将要消失,返回最终浏览的imageview
 @param index 当前显示的下标
 @return 最终浏览的imageview
 */
- (UIView *)photoBrowser:(LJAvatarBrowser *)browser willDissmissAtIndex:(NSInteger)index;

/**
 长按事件
 */
- (void)photoBrowser:(LJAvatarBrowser *)browser longPressAtIndex:(NSInteger)index;

@end

@interface LJAvatarBrowser : UIView

/**
 需要预览的照片数组
 */
@property (nonatomic, retain) NSMutableArray *previewPhotos;

/**
 预览位置
 */
@property (nonatomic, assign) NSInteger previewIndex;

/**
 占位图
 */
@property (nonatomic, weak) UIImage *placeholderImage;

/**
 正在预览的父View
 */
@property (nonatomic, weak) UIView *containerView;

/**
 长按事件
 */
@property (nonatomic, copy) void (^longPressBlock)(NSInteger);

/**
 LJAvatarBrowser
 @param avatarImageView 预览的imageView
 @return LJAvatarBrowser
 */
+ (LJAvatarBrowser *)showImageView:(UIImageView*)avatarImageView;

/**
 LJAvatarBrowser
 @param avatarImageView 预览的imageView
 @param url 原高清地址
 @return LJAvatarBrowser
 */
+ (LJAvatarBrowser *)showImageView:(UIImageView*)avatarImageView originUrl:(NSString *)url;

/**
 查看多placeholder @param previewPhotos 预览数组
 @param containerView 传入的控件的父View
 @param delegate 预览页
 @param previewIndex 预览位置
 @param placeholder 占位图
 */
+ (LJAvatarBrowser *)showPreviewPhotos:(NSMutableArray *)previewPhotos
                              delegate:(id)delegate
                         containerView:(UIView *)containerView
                          previewIndex:(NSInteger)previewIndex
                      placeholderImage:(UIImage *)placeholder;

@end

@interface LJAvatarBrowserImageView : UIImageView

- (void)lj_setImageWithURL:(NSURL *)url placeholderImage:(UIImage *)placeholder completion:(void(^)(void))completion;

@end

@interface LJAvatarBrowserCell : UICollectionViewCell

@end
```  
 
