在用python写code时，遇到了 No module的问题。那python的module是什么？如何正确找到它?

详细的说明请参见python document https://docs.python.org/3.5/tutorial/modules.html.

## Module

Python中的module可以理解成一个后缀为py文件，它可以被其它python文件引用。


## Package

Package是指包含文件 **\__init__.py** 的文件夹。在Python中，是通过在文件夹中放入 init 文件，来告诉Python解释器，要沿这个文件夹继续搜索。

## Python的搜索路径

那么在Python中，是如何搜索一个Module的呢？
是按照**sys.path**中的值来进行搜索的。可以运行python命令查看。

```
$ python
Python 2.7.10 (default, Jul 14 2015, 19:46:27) 
[GCC 4.2.1 Compatible Apple LLVM 6.0 (clang-600.0.39)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> sys.path
['', '/tmp', '/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/PyObjC', '/Library/Python/2.7/site-packages']
```

python会把当前运行的目录加到sys.path 数组的前面，同时也会把PYTHONPATH环境变量的中的值加到sys.path中进行搜索。

1. 首先是在系统build-in的库中搜索。
2. 如果没有找到，就会在当前目录下以及当前目录下的package中进行搜索。
3. 如果没有找到，就会在PYTHONPATH定义的目录中搜索。
4. 如果还没有找到，就在第三方库中进行搜索。

sys.path的值也可以在程序中进行修改，以改变搜索的路径。

## 如何引用兄弟目录下的文件？

假设目录结构是这样的(借用python网站的例子)：

<pre>sound/                          Top-level package
      __init__.py               Initialize the sound package
      formats/                  Subpackage for file format conversions
              __init__.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  Subpackage for sound effects
              __init__.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  Subpackage for filters
              __init__.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...
</pre>

假设现在formats中的auwrite.py，要引用filters中的karaoke.py怎么办呢？
我们可以将sound文件夹加入到搜索的path中，为了防止在程序中动态修改sys.path引来的麻烦，我们可以将sound目录加入到 PYTHONPATH中，这样在搜索Module时，就会在sound目录下进行搜索了。

formats中的 auwrite.py可以通过 from filters.karaoke import *的方式， 引用filter中的文件。

同样在有的IDE中，也会默认**将项目的根目录加到搜索路径中来**，这样解决了找不到Module的问题。