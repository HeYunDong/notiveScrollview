# notiveScrollview
// 开启定时器
- (void)startTimer {
    if (!_timer) {
        _timer = [NSTimer timerWithTimeInterval:_timeInterval target:self selector:@selector(timerMethod) userInfo:nil repeats:YES];
        [[NSRunLoop currentRunLoop] addTimer:_timer forMode:NSRunLoopCommonModes];
    }
}

/// 定时器方法
- (void)timerMethod {
    _count++;
    if (_count == _contents.count) {
        _count = 0;
    }
    /// 两次动画实现类似UIScrollView的滚动效果，控制坐标和隐藏状态
    [UIView animateWithDuration:_scrollTimeInterval animations:^{
        _scrollLbl.frame = CGRectMake(0, -Height, Width, Height);
    } completion:^(BOOL finished) {
        _scrollLbl.hidden = YES;
        _scrollLbl.frame = CGRectMake(0, Height, Width, Height);
        _scrollLbl.hidden = NO;
        [UIView animateWithDuration:_scrollTimeInterval animations:^{
            _scrollLbl.text = [self getCurrentContent];
            _scrollLbl.frame = CGRectMake(0, 0, Width, Height);
        } completion:^(BOOL finished) {
            
        }];
    }];
}
