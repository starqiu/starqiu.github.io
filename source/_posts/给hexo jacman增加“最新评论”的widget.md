title:  给hexo/jacman增加“最新评论”的widget
description: 给hexo/jacman增加“最新评论”的widget
date: 2015-08-30
tags:  [hexo,theme]
categories:  [hexo ]

----
jacman使用了多说的评论系统，多说有最新评论的嵌入代码。当然直接嵌入肯定是不行的，和整体风格不统一看着不好看，那么就搞个类似友情链接、目录之类的widget好了。本文目标是新建一个widget显示多说的最新评论。
# 步骤
## 新建widget
widget 文件在路径`themes/pacman/layout/_widget/`下，参考links.ejs以及archives.ejs及多说的嵌入代码，在该目录下新建一个comment.ejs文件，内容如下：
```javascript
<% if (theme.duoshuo_recent_comment && theme.duoshuo_shortname.length) { %>
<div class="commentslist">
  <p class="asidetitle"><%= __('comments') %></p>
  <ul class="ds-recent-comments" data-num-items="5" data-show-avatars="0" data-show-time="1" data-show-admin="1" data-excerpt-length="32" data-show-title="1"></ul>
</div>
<!--多说js加载开始，一个页面只需要加载一次 -->
<script type="text/javascript">
  var duoshuoQuery = {short_name:"<%= theme.duoshuo.short_name %>"};
  (function() {
    var ds = document.createElement('script');
    ds.type = 'text/javascript';ds.async = true;
    ds.src = 'http://static.duoshuo.com/embed.js';
    ds.charset = 'UTF-8';
    (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(ds);
  })();
</script>
<!--多说js加载结束，一个页面只需要加载一次 -->
<% } %>
```
下面那段js是多说提供的嵌入代码，`<ul>`标签有一些参数可以指定评论的具体数量之类的，大致有以下可选参数
```
 //以下参数均为可选
data-num-items="10"     //显示最新评论的条数，最大支持200条
data-show-avatars="1"   //是否显示头像，1：显示，0：不显示
data-show-time="1"      //是否显示时间，1：显示，0：不显示
data-show-title="0"     //是否显示标题，1：显示，0：不显示
data-show-admin="1"     //是否显示管理员的评论，1：显示，0：不显示
data-excerpt-length="70"//最大显示评论汉字数
```
## 配置widget
1. 首先先添加“最新评论”的多语言版本字符串值
 即用变量comments表示，需要修改的相关文件为themes/pacman/languages/*.yml，看一下文件内容就知道怎么改了
2. 添加一下相关的css样式
 这里是以友情链接widget的css作为基准，稍加修改的，在`themes/pacman/source/css/_partial/aside.styl`文件末尾添加如下内容：
 ```
 //comments
.commentslist
  margin-top 0.5em 
  @media mini
    width 45% 
    float left
    margin 0 5% 0 0 
  @media tablet 
    width 100%
    float none
    margin 1em 0 0 
  ul  
    padding 0.5em 0
    a   
      font-size 1em 
      line-height line-height
      display block
      padding 0
      &:hover
        color color-theme
        transition color .25s

.ds-excerpt
  font-size 1.1em
  color color-theme

.ds-recent-comments
  margin-top -0.6em
  margin-left 0.3em
 ```

## 开启widget
在`themes/jacman/_config.yml`的comment处添加配置`duoshuo_recent_comment: true`
# 参考
[1]： [给hexo/pacman增加“最新评论”的widget](http://odinliu.com/2014/12/03/%E7%BB%99hexo-pacman%E5%A2%9E%E5%8A%A0%E2%80%9C%E6%9C%80%E6%96%B0%E8%AF%84%E8%AE%BA%E2%80%9D%E7%9A%84widget/)