# ZXBannerView
1. 一个无限循环的bannerView，可以使用initWithFrame创建，也可以使用init创建后再使用Masonry进行约束。
2. 使用block方式处理banner图点击事件，可自定义传入block的参数。（修改ZXBannerData）
3. 需要注意的是传入的图片url和link的个数必须相等。
4. 支持横竖屏


# 示例动画
![IntroduceAnimation](https://raw.githubusercontent.com/xzx951753/ZXBannerView/71d9f133f4248ec23ef2330de4cb50c04369520d/IntroduceAnimation.gif "IntroduceAnimation")

# 示例代码
```Objective-C
- (void)viewDidLoad
{
    [super viewDidLoad];
    
    //Can be direct initWithFrame method or init method then masonry constraint.
    ZXBannerView* bannerView = [[ZXBannerView alloc] init];
    [self.view addSubview:bannerView];
    
    [bannerView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.top.right.left.equalTo(self.view);
        make.height.mas_equalTo(220);
    }];
    
    //Image links array
    NSArray* urls = @[@"https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3632476635,370760416&fm=27&gp=0.jpg",
                      @"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1520944054455&di=cc47835e24392e6ffa51463539524301&imgtype=0&src=http%3A%2F%2Fpic2.ooopic.com%2F10%2F57%2F50%2F93b1OOOPIC4d.jpg",
                      @"https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2275205136,3989077551&fm=27&gp=0.jpg",
                      @"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1521024592371&di=f05bd0d4e516f152bf7587ac7c8ebf5b&imgtype=0&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F01164155448e950000019ae95d8b93.jpg"
                      ];
    
    //It sort relative to images array, Through it to tell us you touched which image.
    NSArray* links = @[@"link1",@"link2",@"link3",@"link4"];
    
    NSMutableArray* mutable = [NSMutableArray array];
    for ( NSInteger count = 0 ; count < urls.count ; count++){
        ZXBannerData* data = [[ZXBannerData alloc] init];
        data.url = urls[count];
        data.link = links[count];
        [mutable addObject:data];
    }
    
    [bannerView setImagesWithBannerDatas:mutable
                        withRollInterval:3
                     withAnimateInterval:0.5
              withPageIndicatorTintColor:[UIColor grayColor]
       withCurrentPageIndicatorTintColor:[UIColor redColor]
                          withTouchBlock:^(id  _Nullable data) {
        ZXBannerData* bannerData = (ZXBannerData*)data;
        NSLog(@"link=%@",bannerData.link);
    }];
}
```

## 安装

已上传到trunk，可使用pod安装

```ruby
pod 'ZXBannerView'
```

## Author
如有发现问题，欢迎提交给我!!
Xie zexin, 285644797@qq.com

## License

ZXBannerView is available under the MIT license. See the LICENSE file for more info.

