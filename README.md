# music
歌单列表 
播放歌曲


1. 切换Tab
点击事件---- 监听tab的click 事件，当前的this就是用户点击的tab.
通过index下标找到对应的content，js操作添加content-css状态 。


2. 歌曲列表
ajax --与后台交互，请求对应接口数据
字符串模板---数据替换到模板
sq图标展示---响应数据sq判断,为1时，创建icon加入页面
渲染页面---加入模板到页面位置


3. 播放歌曲--歌曲详情页
流程： 首页--用户点击歌曲--跳转到专属歌曲页面--点击播放按钮---播放音乐

歌曲滚动显示
--大体分两个关键:  
1.audio当前播放时间与歌词时间进行比较，找到当前播放时对应的歌词    
2.计算距离，滚动 tanslateY

步骤：
--setInterval()
--根据当前的路径url来请求相关歌曲数据： 歌名 作者 歌词等
--将数据渲染到页面
--动态创建<audio>,指定audio.src

--歌词特点： 是一段字符串，每段歌词有响应的时间标注，每段都用\n分段

#####1.找到当前播放时对应的歌词

--获取歌词段中的时间   
字符串==split===数组==map整个数组 == 正则表达式找出时间部分== return {time: '12', text: '歌词'}== time部分就是每段歌词时间表示  

-- 获取到audio当前时间 A =  audio.currentTime 
-- 循环遍历所有的p歌词段的所有时间 和当前本身的下一个歌词段
-- 判断 找到 A < 当前歌词段  &&  A <  当前下一个歌词段时间， 只有在这个范围内 找的当前歌曲段才是正在播放的
-- 当前歌曲段加样式

#####2.滚动效果 ----这个要基于找到当前歌曲段
```
// $whichLine 代表当前歌曲段
if ($whichLine) {
                $whichLine.addClass('active').prev().removeClass('active');
                let top = $whichLine.offset().top;
                let linesTop = $('.lines').offset().top;
                let delta = top - linesTop - $('.lyric').height() / 3;
                $('.lines').css('transform', `translateY(-${delta}px`);
}
```


