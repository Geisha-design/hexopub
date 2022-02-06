---
layout: post
title: 主题字体的修改
abbrlink: 22267
date: 2021-08-21 21:30:30
tags:
---



起因：思源宋体真的很好看
需求：将 blog 的标题与正文修改为思源宋体
tips：每一步的目的都是猜的，用词对不对我也不知道，大概理会中心思想就好<!--more-->

步骤：

### 在 Adobe Typekit 网站上注册账号，并且打包字体

网址为：[Adobe Typekit](https://fonts.adobe.com/)
这一步可以让没有安装思源宋体的电脑也能够使用这个字体~~（就是 loading 速度有点慢）~~

1. 右上角注册 Adobe 账号，地区选择 `United states`

2. 登陆后，搜索栏搜索 `Source Han Serif Simplified Chinese` 

3. 点击 </> 按钮，在 `Enter a new project name` 处随便输入一个名字，点击 `Show 5 more` ，选择你需要的字重（建议是 light，Medium 和 bold 这三个。）

4. 点击 `create` 按钮，右上角复制按钮把显示的代码复制下来，备用

   如：

   ```
   <script>
     (function(d) {
       var config = {
         kitId: 'paj7pia',
         scriptTimeout: 3000,
         async: true
       },
       h=d.documentElement,t=setTimeout(function(){h.className=h.className.replace(/\bwf-loading\b/g,"")+" wf-inactive";},config.scriptTimeout),tk=d.createElement("script"),f=false,s=d.getElementsByTagName("script")[0],a;h.className+=" wf-loading";tk.src='https://use.typekit.net/'+config.kitId+'.js';tk.async=true;tk.onload=tk.onreadystatechange=function(){a=this.readyState;if(f||a&&a!="complete"&&a!="loaded")return;f=true;clearTimeout(t);try{Typekit.load(config)}catch(e){}};s.parentNode.insertBefore(tk,s)
     })(document);
   </script>
   ```

到这一步就打包好了，接下来改动 hexo 本地文件夹中的配置文件，使这个代码在 blog 配置文件中生效，也就是让 blog 能够顺利调用[Adobe Typekit](https://fonts.adobe.com/) 网站上你选好的字体。

### 修改 after_footer.pug 文件

这个文件具体干嘛的我也不是很清楚，反正走完这一步 blog 就能用思源宋体了

1. 文件位置在你的 hexo 文件夹 `\themes\maupassant\layout\_partial` 的位置
2. 打开它，拉到最下面，粘贴你刚刚复制的代码
3. 修改最上面的 `<script>` 为 `script.` ，删除最下面的 `<script>` ，注意缩进关系
    这一步改完以后效果应当是这样的：

```
script(type='text/javascript', src=url_for(theme.js) + '/codeblock-resizer.js' + '?v=' + theme.version)
script(type='text/javascript', src=url_for(theme.js) + '/smartresize.js' + '?v=' + theme.version)
script.
  (function(d) {
    var config = {
      kitId: 'wsr0swh',
      scriptTimeout: 3000,
      async: true
    },
    h=d.documentElement,t=setTimeout(function(){h.className=h.className.replace(/\bwf-loading\b/g,"")+" wf-inactive";},config.scriptTimeout),tk=d.createElement("script"),f=false,s=d.getElementsByTagName("script")[0],a;h.className+=" wf-loading";tk.src='https://use.typekit.net/'+config.kitId+'.js';tk.async=true;tk.onload=tk.onreadystatechange=function(){a=this.readyState;if(f||a&&a!="complete"&&a!="loaded")return;f=true;clearTimeout(t);try{Typekit.load(config)}catch(e){}};s.parentNode.insertBefore(tk,s)
  })(document);
```

### 修改 CSS 配置

这一步的目的是让引用的字体文件能应用到 blog 样式里，修改的 `font-family:` 行按顺序读取字体名称进行显示，所以把字体名称加进去的时候要加在最前面

1. 搜索 `pure-g`，找到 `font-family:` 行，在最前面加入 `"source-han-serif-sc", serif,` 
2. 搜索 `body` ，找到 `font-family:` 行，在最前面加入 `"source-han-serif-sc", serif,`
   这一步做完了理论上就完成了，对 blog 进行部署即可

### 我另外做了几件事

1. 搜索了其他的 `font-family:` 段，在其他 `font-family:` 段里加入了字体名称，试图修改掉 page 名的字体，结论失败，这个好像不能在 CSS 文件中进行修改（旋岚：好像这个东西和图标是一套的 ，我们自己能改的是 style.css，它来源于 font-awsome.min.css ）

2. 修改 blog 的字体大小，字体控制分别是以下这几段代码

   全局：搜索 `body` ，修改 `font-size: 15px`，px 就是字体大小
   标题：搜索 `post`，修改 `font: 700 25px/1.1`，
   正文：搜索 `post-content`，修改 `font-size: 15px`，

### 最终思路回顾

在 Adobe Typekit 网站中调用需要的字体→将字体引用代码扔进 blog 本地文件供 blog 使用→修改 CSS 样式文件让 blog 优先显示你选择的字体

### 顺便

改完了以后我用来替代”阅读全文“的小云朵可爱了十八倍！从端庄的淑女云变成了香香软软的面包云！

### 鸣谢

大力感谢旋岚的手把手教程，太麻烦你啦谢谢你教我！！！
