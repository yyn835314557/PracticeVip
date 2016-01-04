# 作用:NSNotificationCenter是专门供程序中不同类间的消息通信而设置的.

- 注册通知:即要在什么地方接受消息
   - `[[NSNotificationCenter defaultCenter]  addObserver:self selector:@selector(mytest:) name:@" mytest" object:nil]; `
   - 参数介绍:
      - addObserver: 观察者,即在什么地方接收通知;
　    - selector: 收到通知后调用何种方法;
　    - name: 通知的名字，也是通知的唯一标示，编译器就通过这个找到通知的。
- 发送通知:调用观察者处的方法。
   - `[[NSNotificationCenter defaultCenter] postNotificationName:@"mytest"　object:searchFriendArray];`
   - 参数：
       - postNotificationName：通知的名字，也是通知的唯一标示，编译器就通过这个找到通知的。
       - object：传递的参数

- 注册方法的写法:

 ```
 (void) mytest:(NSNotification*) notification{
   id obj = [notification object];//获取到传递的对象
 }
 ``` 
 
- 附：注册键盘升启关闭消息
 ```
 //键盘升起
 [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(keyboardWillShow:) name:UIKeyboardWillShowNotification object:nil];
 //键盘降下[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(keyboardWillHide:) name:UIKeyboardWillHideNotification object:nil];

 //看一个程序，里面viewDidLoad中有
 NSNotificationCenter  *center = [NSNotificationCenter defaultCenter];
 [[NSNotificationCenter defaultCenter] removeObserver:self name:@"saveMessage" object:nil];
 [center addObserver:self selector:@selector(saveMessage) name:@"saveMessage" object:nil];
 
//不明白为什么先去掉注册者，然后又添加？不是同一个observer吗？消息傳送机构:举例说明在有需要的类中，发送消息
//发送消息出去，这里的对象是一个数组：saveImageArray
[[NSNotificationCenter defaultCenter] postNotificationName:@"postData" object:saveImageArray];
 
所有亲朋好友给我给包(发送消息)，，，
 
//注册一个observer来响应消息的传送
[[NSNotificationCenter defaultCenter] addObserver:self
                                             selector:@selector(PostImage:)//接收消息方法
                                                 name:@"postData"//消息识别名称
                                               object:nil];
                                                
//举个例子，过年了，准备一个大的钱包(注册一个OBserver)，嘿嘿，
             
                                   
//实现方法
-(void)PostImage:(NSArray *)array
{
    //接收传送过来的消息
}
 
我把红包都收起来，（接收消息）
                                                               
//移除observer
[[NSNotificationCenter defaultCenter] removeObserver:self name:@"postData" object:nil];
红包都收完了，哈哈，亲朋好友回家咯。。
 
 
 
简单说明，哈哈，不需要理解太复杂。。。。
 
例说明：KVC用来传送消息，是很不错的。
 
 
//kvo注册以parserDatas为例说明：parserDatas是一个解析XML的类
[parserDatas addObserver:self 
forKeyPath:@"isFinished"    options:(NSKeyValueObservingOptionNew | 
NSKeyValueObservingOptionOld) context:parserDatas];
 
 
//接收变更通知
- (void)observeValueForKeyPath:(NSString *)keyPath
                      ofObject:(id)object
                        change:(NSDictionary *)change
                       context:(void *)context{
     
    if ([keyPath isEqual:@"isFinished"]) {
        BOOL isFinished=[[change objectForKey:NSKeyValueChangeNewKey] intValue];
        if (isFinished) {//如果服务器数据接收完毕
             
            NSMutableArray *array = [[NSMutableArray alloc] init];
            [array addObjectsFromArray:parserDatas.parsedDataArray];
            //保存数据
            [[UIApplication sharedApplication] setNetworkActivityIndicatorVisible:NO];
            NSString *path = [DOCUMENT_PATH stringByAppendingPathComponent:@"AllXmlDataArray.bin"];
            [NSKeyedArchiver archiveRootObject:array toFile:path];
            [array release];
            //取消kvo注册
            [object removeObserver:self
                     forKeyPath:@"isFinished"];
        }      
    }else{
        // be sure to call the super implementation
        // if the superclass implements it
        [super observeValueForKeyPath:keyPath
                             ofObject:object
                               change:change
                              context:context];
    }
}
 
 
 
在parserDatas类中定义：
 
+ (BOOL):(NSString*)key
{
    //当这两个值改变时，使用自动通知已注册过的观察者，观察者需要实现observeValueForKeyPath:ofObject:change:context:方法
    if ([key isEqualToString:@"isFinished"])
    {
        return YES;
    }
    return [super automaticallyNotifiesObserversForKey:key];
}
 
 
 
发送变更通知：
 
在需要跟踪消息记录的函数中加入：
[self setValue:[NSNumber numberWithBool:YES] forKey:@"isFinished"];
 
 [[NSNotificationCenter defaultCenter] removeObserver:self name:@"saveMessage" object:nil];
 
不用的时候，才注销掉的。。
 
一般放在dealloc....里面。
 
 
 
在用之前把notification注册掉，是为了防止多次注册，这一般是因为这个view在程序运行时要load很多次，比如Three20
的非顶层的View每次显示的时候都重新load，这样如果不在用之前把notification注册掉，就会重复注册消息，比如每次接收到消息就打印一
句话，当你打开了n次这个view的时候，这句话就会打印n次...
  
- (void)awakeFromNib{
[[NSNotificationCenter defaultCenter] addObserver:self
selector:@selector(switchViews:)
name:@"switchViews"
  object:nil];
}
  
- (void)switchViews:(NSNotification*)notification{
NSNumber *viewNumber = [notification object];
NSInteger i = [viewNumber integerValue];
[self setSelectedSegmentIndex:i];
UIView *chosenView = nil;
switch (i) {
case 0:
chosenView = view1;
break;
case 1:
chosenView = view2;
break;
case 2:
chosenView = view3;
break;
default:
break;
}
if (chosenView) {
[[viewController view] bringSubviewToFront:chosenView];
}
}
  
- (void)dealloc{
[super dealloc];
[[NSNotificationCenter defaultCenter] removeObserver:self];
}
  
@end