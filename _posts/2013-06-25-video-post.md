---
layout: post
title:  "抛飞/一键起飞"
date:   2017-09-11
excerpt: "GG飞行器的抛飞与一键起飞，降落部分请自动忽略"
tag:
- sample
- post
- video
comments: true
---

<iframe width="854" height="480" src="https://www.youtube.com/embed/Y8GasuT7-Qs" frameborder="0" allowfullscreen></iframe>
Video embeds are responsive and scale with the width of the main content block with the help of [FitVids](http://fitvidsjs.com/).

Not sure if this only effects Kramdown or if it's an issue with Markdown in general. But adding YouTube video embeds causes errors when building your Jekyll site. To fix add a space between the `<iframe>` tags and remove `allowfullscreen`. Example below:

{% highlight html %}
贴视频只需 翻墙 把视频上传到YouTube 打开视频 右键 复制嵌入代码 贴上来 ok
{% endhighlight %}

下面几个label我还不知道怎么搞，先放在那儿吧
