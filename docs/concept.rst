
======================
    Concept 概念
======================

In order to keep test execution efficient when number of test
cases grows, it is crucial to maintain corresponding metadata,
which define some aspects of how the test coverage is executed.
``#>>>``
为了在测试用例数量增长时保持测试执行效率，维护相应的元数据至关重要，
这些元数据定义了测试覆盖率执行方式的某些方面。

This tool implements a flexible format for defining metadata in
plain text files which can be stored close to the test code and
structured in a hierarchical way with support for inheritance.
``#>>>``
该工具实现了一种灵活的格式，用于在纯文本文件中定义元数据，
这些文件可以靠近测试代码存储，并以支持继承的分层方式构建。


Although the proposal initially originated from user stories
centered around test execution, the format is general and thus
can be used in broader scenarios, e.g. test coverage mapping.
``#>>>``
尽管该提案最初起源于以测试执行为中心的用户故事，但格式是通用的，
因此可以用于更广泛的场景，例如测试覆盖映射。

Using this approach it's also possible to combine both test
execution metadata and test coverage information. Thanks to
elasticity and hierarchy it provides ability to organize data
into well-sized text documents while preventing duplication.
``#>>>``
使用这种方法，还可以结合测试执行元数据和测试覆盖率信息。
由于弹性和层次结构，它提供了将数据组织成大小适中的文本文档的能力，
同时防止重复。


Stones 里程碑
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These are essential corner stones for the design:
``#>>>``
设计的基本基石：

* Text files under version control
  ``#>>>``
  基于版本控制的文本文件
* Keep common uses cases simple
  ``#>>>``
  保持常见的用例简单
* Use hierarchy to organize content
  ``#>>>``
  使用层次结构来组织内容
* Prevent duplication where possible
  ``#>>>``
  尽可能防止重复
* Metadata close to the test code
  ``#>>>``
  让元数据靠近测试代码
* Solution should be open source
  ``#>>>``
  解决方案应该是开源的
* Focus on essential use cases
  ``#>>>``
  专注于基本用例


Stories 故事
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Important user stories to be covered:
``#>>>``
要涵盖的重要用户故事：

* As a tester or developer I want to easy read and modify metadata and see history.
  ``#>>>``
  作为测试人员或开发人员，我想轻松阅读和修改元数据并查看历史记录。
* As a tester I want to select a subset of test cases for execution by specifying a tag.
  ``#>>>``
  作为测试人员，我想通过指定标签来选择要执行的测试用例的子集。
* As a tester I want to define a maximum time for a test case to run.
  ``#>>>``
  作为测试人员，我想定义测试用例运行的最长时间。
* As a tester I want to specify which environment is relevant for testing.
  ``#>>>``
  作为测试人员，我想指定与测试相关的环境。
* As a user I want to easily define common metadata for multiple cases to simplify maintenance.
  ``#>>>``
  作为用户，我想轻松地为多个案例定义通用元数据以简化维护。
* As a user I want to provide specific metadata for selected tests to complement common metadata.
  ``#>>>``
  作为用户，我想为选定的测试提供特定的元数据以补充通用元数据。
* As an individual tester and test contributor I want to execute specific single test case.
  ``#>>>``
  作为个人测试人员和测试贡献者，我想执行特定的单个测试用例。
* As an automation tool I need a metadata storage with good api, extensible, quick for reading.
  ``#>>>``
  作为一个自动化工具，我需要一个具有良好API、可扩展、快速阅读的元数据存储。


Choices 选择
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These choices have been made:
``#>>>``
FMF做出了这些选择：

* Use git for version control and history of changes.
  ``#>>>``
  使用git进行版本控制和更改历史记录。
* Yaml format easily readable for both machines and humans.
  ``#>>>``
  YAML格式易于机器和人类阅读。


Files 文件
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A dedicated file name extension ``fmf`` as an abbreviation of
Flexible Metadata Format is used to easily find all metadata
files on the filesystem:
``#>>>``
专用文件扩展名
``fmf``
作为
``Flexible Metadata Format``
的缩写，用于轻松查找文件系统上的所有元数据文件：

* smoke.fmf
* main.fmf

Special file name ``main.fmf`` works similarly as ``index.html``.
It can be used to define the top level data for the directory. All
metadata files are expected to be using the ``utf-8`` encoding.
``#>>>``
特殊文件名
``main.fmf``
的工作方式与
``index.html``
类似。它可用于定义目录的顶级数据。所有元数据文件都应使用
``utf-8``
编码。


Attributes 属性
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The format does not define attribute naming in any way. This is up
to individual projects. The only exception is the special name
``main`` which is reserved for main directory index.
``#>>>``
该格式不以任何方式定义属性命名。这取决于个别项目。
唯一的例外是为主目录索引保留的特殊名称
``main``
。

Attribute namespacing can be introduced as needed to prevent
collisions between similar attributes. For example:
``#>>>``
可以根据需要引入属性命名空间，以防止相似属性之间的冲突。 例如：

* test-description, requirement-description
* test:description, requirement:description
* test_description, requirement_description


Trees 树
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Metadata form a tree where inheritance is applied. The tree root
is defined by an ``.fmf`` directory (similarly as ``.git``
identifies top of the git repository). The ``.fmf`` directory
contains at least a ``version`` file with a single integer number
defining version of the format.
``#>>>``
元数据形成一棵应用继承的树。
树根由
``.fmf``
目录定义（类似于
``.git``
标识git存储库的顶部）。
``.fmf``
目录至少包含一个版本文件，其中包含一个定义格式版本的整数。


Names 命名
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Individual tree nodes are identified by path from the metadata
root directory plus optional hierarchy defined inside yaml files.
For example, let's have the metadata root defined in the ``wget``
directory. Below you can see node names for different files:
``#>>>``
各个树节点由元数据根目录的路径加上YAML文件中定义的可选层次结构标识。
例如，让我们在
``wget``
目录中定义元数据根目录。 您可以在下面看到不同文件的节点名称：

    +-------------------------------+-----------------------+
    | Location                      | Name                  |
    +===============================+=======================+
    | wget/main.fmf                 | /                     |
    +-------------------------------+-----------------------+
    | wget/download/main.fmf        | /download             |
    +-------------------------------+-----------------------+
    | wget/download/smoke.fmf       | /download/smoke       |
    +-------------------------------+-----------------------+


Identifiers 身份标识
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Node names are unique across the metadata tree and thus can be
used as identifiers for local referencing across the same tree. In
order to reference remote fmf nodes from other trees a full ``fmf
identifier`` is defined as a dictionary containing keys with the
following meaning:
``#>>>``
节点名称在整个元数据树中是唯一的，因此可以用作跨同一棵树的本地引用的标识符。
为了从其他树引用远程FMF节点，完整的
``FMF标识符``
被定义为包含具有以下含义的键的字典：

url
    Git repository containing the metadata tree. Use any format
    acceptable by the ``git clone`` command. Optional, if no
    repository url is provided, local files will be used.
    ``#>>>``
    包含元数据树的Git存储库。使用
    ``git clone``
    命令可接受的任何格式。可选地，如果未提供存储库url，将使用本地文件。
ref
    Branch, tag or commit specifying the desired git revision.
    This is used to perform a ``git checkout`` in the repository.
    If not provided, the ``default branch`` is used.
    ``#>>>``
    指定所需的git修订版的分支、标记或提交。 这用于在存储库中执行
    ``git checkout``
    。 如果未提供，则使用
    ``默认分支``
    。
path
    Path to the metadata tree root. Should be relative to the git
    repository root if ``url`` provided, absolute local filesystem
    path otherwise. Optional, by default ``.`` is used.
    ``#>>>``
    元数据树根的路径。 如果提供了
    ``url``
    ，应该是相对于git存储库根目录的，否则是绝对本地文件系统路径。可选地，默认情况下使用
    ``.``
    。
name
    Node name as defined by the hierarchy in the metadata tree.
    Optional, by default the parent node ``/`` is used, which
    represents the whole metadata tree.
    ``#>>>``
    由元数据树中的层次结构定义的节点名称。可选地，默认使用父节点
    ``/``
    ，它代表整个元数据树。

Here's a full fmf identifier example::
``#>>>``
这是一个完整的 fmf 标识符示例::

    url: https://github.com/psss/fmf
    ref: 0.10
    path: /examples/wget
    name: /download/test

Use default values for ``ref`` and ``path`` to reference the
latest version of the smoke plan from the default branch::
``#>>>``
使用
``ref``
和
``path``
的默认值从默认分支引用最新版本的烟雾计划:: 

    url: https://github.com/psss/fmf
    name: /plans/smoke

If desired, it is also possible to write the identifier on a
single line as supported by the ``yaml`` format::
``#>>>``
如果需要，也可以在
``yaml``
格式支持的情况下将标识符写在一行中::

    {url: "https://github.com/psss/fmf", name: "/plans/smoke"}

Let's freeze the stable test version by using a specific commit::
``#>>>``
让我们通过使用特定的提交来冻结稳定的测试版本::

    url: https://github.com/psss/fmf
    ref: f24ef3f
    name: /tests/basic/filter

Reference a smoke plan from another metadata tree stored on the
local filesystem::
``#>>>``
从存储在本地文件系统上的另一个元数据树引用冒烟计划::

    path: /home/psss/git/tmt
    name: /plans/smoke

Local reference across the same metadata tree is also supported::
``#>>>``
还支持跨同一元数据树的本地引用::
    name: /plans/smoke
