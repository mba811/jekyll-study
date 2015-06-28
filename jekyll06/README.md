#  Liquid 模板

Jekyll 使用 [Liquid](http://liquidmarkup.org/) 来处理模板数据。除了 [标准的Liquid标签和过滤器](https://github.com/shopify/liquid/wiki/liquid-for-designers)，Jekyll还增加一些它自己特有的：

#### 过滤器

**日期-XML**

将时间转换成 XML 格式
    
    {{ site.time | date_to_xmlschema }} => 2008-11-17T13:07:54-08:00
    

**日期-字符串**

将时间转换成短格式，举例："27 Jan 2011"。
    
    {{ site.time | date_to_string }} => 17 Nov 2008
    

**日期-长字符串**

将时间转换成长格式，举例："27 January 2011"。
    
    {{ site.time | date_to_long_string }} => 17 November 2008
    

**XML转义**

在 XML 中的转义字符。
    
    {{ page.content | xml_escape }}
    

**CGI 转义字符**

CGI 会在 URL 中将一个字符串转义。用正确的 %XX 替换所有特殊字符。
    
    {{ "foo,bar;baz?" | cgi_escape }} => foo%2Cbar%3Bbaz%3F
    

**单词数**

在文本统计单词的数目。
    
    {{ page.content | number_of_words }} => 1337
    

**数组-句子**

讲一个数组转换成一个句子。
    
    {{ page.tags | array_to_sentence_string }} => foo,bar,and baz
    

**Textilize**

将一个 Textilize 格式的字符串转换成 HTML 格式，通过 RedCloth 渲染的。
    
    {{ page.excerpt | textilize }}
    

**Markdownify**

将一个 Markdown 格式的文件转换成 HTML 格式。
    
    {{ page.excerpt | markdownify }}
    

#### 标签

**Include**

如果你有小的页面框架碎片需要添加到你站点上多个不同的文件中，你可以使用 `inlcude` 标签。
    
    {% include sig.textile %}
    

Jekyll 总是从你根目录下的 `_include` 目录下寻找需要加载的文件。

**代码高亮**

Jekyll 通过 Pygments 内建支持了代码高亮，支持超过 [100种语言](http://pygments.org/languages/)。为了使这个机制，你需要安装 Pygments，而且 pygmentize 的可执行文件必须在你 `path` 路径中，当你运行 Jekyll 时，确保以 Pygments 支持的方式运行。

为了表示一个需要高亮的代码块，你需要：
    
    {% highlight ruby %}
    def foo
        puts 'foo'
    end
    {% endhighlight %}
    

`highlight` 的参数是一个编程语言的标示符，你可以在 [Lexers](http://pygments.org/docs/lexers/) 上找到你所喜欢的编程语言的正确标示符。

**行号**

`highlight` 有第二个叫做 `linenos` 的参数，这是一个可选的选项，使用这个选项可以使高亮的代码加入行号。举例来说，下面的代码段块将会在每行的行首加入行号。
    
    {% highlight ruby linenos %}
    def foo
        puts 'foo'
    end
    {% endhighlight %}
    

为了使你的代码高亮生效，你需要引入高亮的层叠样式表(就是 CSS 文件—译者注)。[这里](http://github.com/mojombo/tpw/tree/master/css/syntax.css) 是一个样式表的例子。这个样式表也正是 GitHub 所使用的，你可以在你的站点免费地使用它。如果你要使用行号，你需要在你样式表中添加一个额外的 CSS 类定义，以此来区分行号和高亮的代码。

**博文的 Url**

如果你想要在一篇文章中加入一个链接，你可以使用`post_tag`标签。
    
    {% post_url 2010-07-21-name-of-post %}
    

可以通过以下的方式来创建一个链接：
    
    [Name of Link]({% post_url 2010-07-21-name-of-post %})
