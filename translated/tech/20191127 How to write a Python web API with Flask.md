[#]: collector: (lujun9972)
[#]: translator: (hj24)
[#]: reviewer: ( )
[#]: publisher: ( )
[#]: url: ( )
[#]: subject: (How to write a Python web API with Flask)
[#]: via: (https://opensource.com/article/19/11/python-web-api-flask)
[#]: author: (Rachel Waston https://opensource.com/users/rachelwaston)

如何使用Flask编写Python Web API
======

这是一个快速教程，用来展示如何通过Flask（目前发展最迅速的Python框架之一）来从服务器获取数据。
![spiderweb diagram][1]

[Python][2]是一个以语法简洁著称的高级的，面向对象的程序语言。它一直都是一个用来构建RESTful API的顶级编程语言。

[Flask][3]是一个高度可定制化的Python框架，可以为开发人员提供用户访问数据方式的完全控制。Flask是一个基于Werkzeug的[WSGI][4]工具包和Jinja 2模板引擎的”微框架“。它是一个被设计来开发RESTful API的web框架。

Flask是Python发展最迅速的框架之一，很多知名网站如：Netflix, Pinterest, 和LinkedIn都将Flask纳入了它们的开发技术栈。下面是一个简单的示例，展示了Flask是如何允许用户通过HTTP GET请求来从服务器获取数据的。

### 初始化一个Flask应用

首先，创建一个你的Flask项目的目录结构。你可以在你系统的任何地方来做这件事。


```
$ mkdir tutorial
$ cd tutorial
$ touch main.py
$ python3 -m venv env
$ source env/bin/activate
(env) $ pip3 install flask-restful
Collecting flask-restful
Downloading <https://files.pythonhosted.org/packages/17/44/6e49...8da4/Flask\_RESTful-0.3.7-py2.py3-none-any.whl>
Collecting Flask&gt;=0.8 (from flask-restful)
[...]
```

### 导入Flask模块

Next, import the **flask** module and its **flask_restful** library into your **main.py** code:

然后，在你的**main.py**代码中导入**flask**模块和它的**flask_restful**库：


```
from flask import Flask
from flask_restful import Resource, Api

app = Flask(__name__)
api = Api(app)

class Quotes(Resource):
    def get(self):
        return {
            'William Shakespeare': {
                'quote': ['Love all,trust a few,do wrong to none',
                'Some are born great, some achieve greatness, and some greatness thrust upon them.']
        },
        'Linus': {
            'quote': ['Talk is cheap. Show me the code.']
            }
        }

api.add_resource(Quotes, '/')

if __name__ == '__main__':
    app.run(debug=True)
```

### 运行app

Flask includes a built-in HTTP server for testing. Test the simple API you built:

Flask包含一个内建的用于测试的HTTP服务器。来测试一下这个你创建的简单的API：


```
(env) $ python main.py
 * Serving Flask app "main" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Running on <http://127.0.0.1:5000/> (Press CTRL+C to quit)
```

启动开发服务器时将启动Flask应用程序，该应用程序包含一个名为 **get** 的方法来响应简单的HTTP GET请求。你可以通过 **wget**、**curl** 命令或者任意的web浏览器来测试它。


```
$ curl <http://localhost:5000>
{
    "William Shakespeare": {
        "quote": [
            "Love all,trust a few,do wrong to none",
            "Some are born great, some achieve greatness, and some greatness thrust upon them."
        ]
    },
    "Linus": {
        "quote": [
            "Talk is cheap. Show me the code."
        ]
    }
}
```

要查看使用Python和Flask的类似Web API的更复杂版本，请导航至美国国会图书馆的[Chronicling America] [5]网站，该网站可提供有关这些信息的历史报纸和数字化报纸。

### 为什么使用 Flask?

Flask有以下几个主要的优点：

  1. Python很流行并且广泛被应用，所以任何熟悉Python的人都可以使用Flask来开发。
  2. 它轻巧而简约。
  3. 考虑安全性而构建。
  4. 出色的文档，其中包含大量清晰，有效的示例代码。

还有一些潜在的缺点:

  1. 它轻巧而简约。但如果您正在寻找具有大量捆绑库和预制组件的框架，那么这可能不是最佳选择。
  2. 如果必须围绕Flask构建自己的框架，则你可能会发现维护自定义项的成本可能会抵消使用Flask的好处。


如果您要构建Web程序或API，可以考虑选择Flask。它功能强大且健壮，并且其优秀的项目文档使入门变得容易。试用一下，评估一下，看看它是否适合您的项目。

在本课中了解更多信息关于Python异常处理以及如何以安全的方式进行操作。

--------------------------------------------------------------------------------

via: https://opensource.com/article/19/11/python-web-api-flask

作者：[Rachel Waston][a]
选题：[lujun9972][b]
译者：[hj24](https://github.com/hj24)
校对：[校对者ID](https://github.com/校对者ID)

本文由 [LCTT](https://github.com/LCTT/TranslateProject) 原创编译，[Linux中国](https://linux.cn/) 荣誉推出

[a]: https://opensource.com/users/rachelwaston
[b]: https://github.com/lujun9972
[1]: https://opensource.com/sites/default/files/styles/image-full-size/public/lead-images/web-cms-build-howto-tutorial.png?itok=bRbCJt1U (spiderweb diagram)
[2]: https://www.python.org/
[3]: https://palletsprojects.com/p/flask/
[4]: https://en.wikipedia.org/wiki/Web_Server_Gateway_Interface
[5]: https://chroniclingamerica.loc.gov/about/api