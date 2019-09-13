---
title: JavaScript 扩展中的本机调试器对象-设计和测试注意事项
description: 本机调试器对象表示调试器环境的各种构造。 本主题介绍 JavaScript 扩展中的本机调试器对象的设计和测试注意事项。
ms.assetid: A8E12564-D083-43A7-920E-22C4D627FEEA
ms.date: 09/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 579efb8f4b693b9c4c42437896eef5edbf3cc368
ms.sourcegitcommit: 3b7c8b3cb59031e0f4e39dac106c1598ad108828
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2019
ms.locfileid: "70935898"
---
# <a name="native-debugger-objects-in-javascript-extensions---design-and-testing-considerations"></a>JavaScript 扩展中的本机调试器对象-设计和测试注意事项

本主题介绍使用 JavaScript 扩展中的本机调试器对象时的设计和测试注意事项。

本机调试器对象表示调试器环境的各种构造和行为。 对象可传递到 JavaScript 扩展中（或在中获取）以操作调试器的状态。

有关调试器对象 JavaScript 扩展的信息，请参阅[Javascript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)。

有关使用 JavaScript 的常规信息，请参阅[Javascript 调试器脚本](javascript-debugger-scripting.md)。

## <a name="span-iddesign-considerationsspanspan-iddesign-considerationsspanspan-iddesign-considerationsspandebugger-data-model-design-considerations"></a><span id="Design-Considerations"></span><span id="design-considerations"></span><span id="DESIGN-CONSIDERATIONS"></span>调试器数据模型设计注意事项

**设计原则**

请考虑以下原则，使调试器扩展提供可发现、可查询和可编写脚本的信息。

-   信息接近所需的位置。 例如，有关注册表项的信息应显示为包含注册表项句柄的局部变量。
-   信息结构化。 例如，有关注册表项的信息显示在单独的字段中，如项类型、密钥 ACL、密钥名称和值。 这意味着可以在不分析文本的情况下访问各个字段。
-   信息一致。 有关注册表项句柄的信息以类似方式提供给有关文件句柄的信息。

避免这些不支持这些原则的方法。

-   不要将项目构建为单一平面 "厨房 sink"。 组织的层次结构允许用户浏览他们查找的信息，而无需事先了解他们所查找的内容并支持可发现性。
-   不要转换经典 dbgeng 扩展，只需将其移动到模型，同时仍输出原始文本的屏幕即可。 这不能与其他扩展组合，且不能通过 LINQ 表达式进行查询。 而是将数据分解为单独的可查询字段。

**命名规则**

-   字段的大小写应为 PascalCase。 对于在其他大小写中普遍已知的名称（如 jQuery），可以考虑使用异常。
-   避免使用通常不会在C++标识符中使用的特殊字符。 例如，避免使用诸如 "总长度" （包含空格）或 "\[大小\]" （包含方括号）之类的名称。 使用此约定，可以更方便地使用脚本语言，其中不允许将这些字符作为标识符的一部分，还可以从命令窗口中更轻松地使用。

**组织和层次结构准则**

-   不要扩展调试器命名空间的顶层。 相反，应在调试器中扩展现有节点，以便在其最相关的位置显示信息。
-   不要重复概念。 如果创建的数据模型扩展列出了有关调试器中已存在的概念的其他信息，请扩展现有信息，而不是尝试将其替换为新信息。 换句话说，显示有关模块的详细信息的扩展应扩展现有*模块*对象，而不是创建新的模块列表。
-   自由浮动实用程序命令必须是调试程序 *. 实用工具*命名空间的一部分。 它们还应带命名空间（例如，FromListEntry）的子*集合*。

**向后兼容性和重大更改**

发布的脚本不应中断与其他依赖于它的脚本的兼容性。 例如，如果将某个函数发布到该模型，则该函数应保留在同一位置并且具有相同的参数（如果可能）。

**不使用外部资源**

-   扩展不能生成外部进程。 外部进程可能会干扰调试器的行为，并将在各种远程调试器方案中错误行为（例如 dbgsrv 远程、ntsd 远程和 "ntsd-d remote"）
-   扩展不能显示任何用户界面。 显示用户界面元素对于远程调试方案的行为不正确，可能会中断控制台调试方案。
-   扩展不能通过未记录的方法来操作调试器引擎或调试器 UI。 这会导致兼容性问题，并在具有不同 UI 的调试器客户端上正常运行。
-   扩展只能通过记录的调试器 Api 访问目标信息。 尝试通过 win32 Api 访问有关目标的信息将对许多远程方案失败，甚至在安全边界内实现某些本地调试方案。

**不使用 Dbgeng 的特定功能**

旨在用作扩展的脚本不得依赖于 dbgeng 特定的功能（例如，执行 "经典" 调试器扩展）。 脚本应该在承载数据模型的任何调试器的顶层使用。

## <a name="span-idtesting-debugger-extensionsspanspan-idtesting-debugger-extensionsspanspan-idtesting-debugger-extensionsspantesting-debugger-extensions"></a><span id="Testing-Debugger-Extensions"></span><span id="testing-debugger-extensions"></span><span id="TESTING-DEBUGGER-EXTENSIONS"></span>测试调试器扩展


扩展应在各种情况下工作。 虽然某些扩展可能特定于某个方案（如内核调试方案），但大多数扩展应在所有方案中都有效，或者具有指示支持的方案的元数据。

内核模式

-   实时内核调试
-   内核转储调试

用户模式

-   实时用户模式调试
-   用户模式转储调试

此外，请考虑这些调试器使用方案

-   多进程调试
-   多会话调试（例如，在单个会话中转储 + 实时用户）

**远程调试器使用情况**

使用远程调试器使用方案测试正确的操作。

-   dbgsrv 远程
-   ntsd 远程
-   ntsd-d 远程

有关详细信息，请参阅[使用 CDB 和 NTSD 进行调试](debugging-using-cdb-and-ntsd.md)和[**激活进程服务器**](activating-a-process-server.md)。

**回归测试**

在发布新版本的调试器的情况下，调查可以验证扩展功能的测试自动化的使用情况。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[JavaScript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)

 [JavaScript 扩展中的本机调试器对象-调试器对象的详细信息](native-objects-in-javascript-extensions-debugger-objects.md)。

[JavaScript 调试器脚本](javascript-debugger-scripting.md)

[JavaScript 调试器示例脚本](javascript-debugger-example-scripts.md)

 

 






