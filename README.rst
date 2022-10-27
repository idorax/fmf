
======================
    fmf
======================

Flexible Metadata Format
``#>>>``
灵活的元数据格式

Description 描述
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The ``fmf`` Python module and command line tool implement a
flexible format for defining metadata in plain text files which
can be stored close to the source code and structured in a
hierarchical way with support for inheritance.
``#>>>``
Python模块
``fmf``
和命令行工具实现了一个用于在纯文本文件中定义元数据的灵活格式，
它可以存储在靠近源代码的位置，并以支持继承的分层方式结构化。

Although the proposal initially originated from user stories
centered around test execution, the format is general and thus
can be used in broader scenarios, e.g. test coverage mapping.
``#>>>``
尽管该提案最初源于以测试执行为中心的用户故事，但格式是通用的，
因此可以用于更广泛的场景，例如 测试覆盖映射。

Using this approach it's also possible to combine both test
execution metadata and test coverage information. Thanks to
elasticity and hierarchy it provides ability to organize data
into well-sized text documents while preventing duplication.
``#>>>``
使用这种方法，还可以结合测试执行元数据和测试覆盖率信息。
由于弹性和层次结构，它提供了将数据组织成大小合适的文本文档的能力，同时防止重复。

Synopsis 概要
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Command line usage is straightforward
``#>>>``
命令行用法很简单::

    fmf command [options]

There are following commands available
``#>>>``
可用命令如下::

    fmf ls      List identifiers of available objects
                列出可用对象的标识符
    fmf show    Show metadata of available objects
                显示可用对象的元数据
    fmf init    Initialize a new metadata tree
                初始化一个新的元数据树
    fmf clean   Remove cache directory and its content
                删除缓存目录及其内容


Examples 示例
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

List names of all objects stored in the metadata tree
``#>>>``
列出存储在元数据树中的所有对象的名称::

    fmf ls

Show all test metadata (with 'test' attribute defined)
``#>>>``
显示所有测试元数据（定义了"测试"属性）::

    fmf show --key test

Show metadata for all tree nodes (not only leaves)
``#>>>``
显示所有树节点的元数据（不仅是叶子）::

    fmf show --key test --whole

List all attributes for the ``/recursion`` tests
``#>>>``
列出
``/recursion``
测试的所有属性::

    fmf show --key test --name /recursion

Show all covered requirements
``#>>>``
显示所有涵盖的要求::

    fmf show --key requirement --key coverage

Search for all tests with the ``Tier1`` tag defined and show a
brief summary of what was found
``#>>>``
搜索定义了Tier1标签的所有测试，并显示所找到内容的简短摘要::

    fmf show --key test --filter tags:Tier1 --verbose

Use arbitrary Python expressions to access deeper objects and
create more complex conditions
``#>>>``
使用任意 Python 表达式来访问更深层次的对象并创建更复杂的条件::

    fmf show --condition "execute['how'] == 'shell'"

Initialize a new metadata tree in the current directory
``#>>>``
在当前目录中初始化一个新的元数据树::

    fmf init

Check help message of individual commands for the full list of
available options.
``#>>>``
检查各个命令的帮助消息以获取可用选项的完整列表。

Options 选项
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Here is the list of the most frequently used options.
``#>>>``
以下是最常用选项的列表。

Select 查询
------

Limit which metadata should be listed.
``#>>>``
限制应列出哪些元数据。

--key=KEYS
    Key content definition (required attributes)
    ``#>>>``
    关键内容定义（必需属性）

--name=NAMES
    List objects with name matching regular expression
    ``#>>>``
    列出名称匹配正则表达式的对象

--filter=FLTRS
    Apply advanced filter when selecting objects
    ``#>>>``
    选择对象时应用高级过滤器

--condition=EXPR
    Use arbitrary Python expression for filtering
    ``#>>>``
    使用任意 Python 表达式进行过滤

--whole
    Consider the whole tree (leaves only by default)
    ``#>>>``
    考虑整棵树（默认情况下只有叶子节点）

For filtering regular expressions can be used as well. See
``pydoc fmf.filter`` for advanced filtering options.
``#>>>``
也可以使用正则表达式过滤。有关高级过滤选项，请参阅
``pydoc fmf.filter``
。

Format 格式
------

Choose the best format for showing the metadata.
``#>>>``
选择显示元数据的最佳格式。

--format=FMT
    Custom output format using the {} expansion
    ``#>>>``
    使用 {} 扩展的自定义输出格式

--value=VALUES
    Values for the custom formatting string
    ``#>>>``
    自定义格式字符串的值

See online documentation for details about custom format.
``#>>>``
有关自定义格式的详细信息，请参阅在线文档。

Utils 实用程序
-----

Various utility options.
``#>>>``
各种实用程序选项。

--path PATHS
    Path to the metadata tree (default: current directory)
    ``#>>>``
    元数据树的路径（默认为当前目录）

--verbose
    Print additional information standard error output
    ``#>>>``
    打印附加信息到标准错误

--debug
    Turn on debugging output, do not catch exceptions
    ``#>>>``
    开启调试输出，不捕获异常

Check help message of individual commands for the full list of
available options.
``#>>>``
检查各个命令的帮助消息以获取可用选项的完整列表。

Install 安装
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The fmf package is available in Fedora and EPEL
``#>>>``
fmf 包在Fedora和EPEL中可用::

    dnf install fmf

Install the latest version from the Copr repository
``#>>>``
从Copr存储库安装最新版本::

    dnf copr enable psss/fmf
    dnf install fmf

or use PIP
``#>>>``
或使用PIP::


    pip install fmf

See documentation for more details about installation options.
``#>>>``
有关安装选项的更多详细信息，请参阅文档。


Variables 变量
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Here is the list of environment variables understood by fmf:
``#>>>``
这里是fmf支持的环境变量列表:

FMF_CACHE_DIRECTORY
    Directory used to cache git clone calls for fmf identifiers.
    ``#>>>``
    用于缓存fmf标识符的git clone调用的目录


Links 链接
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Git:
https://github.com/psss/fmf

Docs:
http://fmf.readthedocs.io/

Issues:
https://github.com/psss/fmf/issues

Releases:
https://github.com/psss/fmf/releases

Copr:
http://copr.fedoraproject.org/coprs/psss/fmf

PIP:
https://pypi.org/project/fmf/

Travis:
https://travis-ci.org/psss/fmf

Coveralls:
https://coveralls.io/github/psss/fmf


Authors 作者
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Petr Šplíchal, Miro Hrončok, Jakub Krysl, Jan Ščotka, Alois
Mahdal, Cleber Rosa, Miroslav Vadkerti, Lukáš Zachar, František
Nečas, Evgeny Fedin and Pablo Martin.


Copyright 版权
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Copyright (c) 2018-2021 Red Hat, Inc.

This program is free software; you can redistribute it and/or
modify it under the terms of the GNU General Public License as
published by the Free Software Foundation; either version 2 of
the License, or (at your option) any later version.
``#>>>``
该程序是自由软件；您可以根据自由软件基金会发布的GNU通用公共许可条款重新分发和（或）修改它；
选择许可证的第二版或更高版本均可。
