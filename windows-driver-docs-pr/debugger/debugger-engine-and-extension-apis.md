---
title: 调试器引擎和扩展 API
description: 调试器引擎和扩展 API
ms.assetid: 2d651c4b-e123-4285-b69c-d7fd5e1f9a81
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 443244ffa091e6f502375d56fed959cf4e55e9c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368128"
---
# <a name="debugger-engine-and-extension-apis"></a>调试器引擎和扩展 API


本部分包括：

[调试器引擎概述](debugger-engine-overview.md)

[使用调试器引擎 API](using-the-debugger-engine-api.md)

[编写 DbgEng 扩展](writing-dbgeng-extensions.md)

[EngExtCpp 扩展](engextcpp-extensions.md)

[编写 WdbgExts 扩展](writing-wdbgexts-extensions.md)

[自定义调试器使用 DML 的输出](#dml)

[使用 JavaScript 来扩展调试器的功能](#javascript)

## <span id="ddk_introduction_dbx"></span><span id="DDK_INTRODUCTION_DBX"></span>


本文档介绍如何使用调试器引擎以及如何编写将在 WinDbg、 KD、 CDB 和 NTSD 中运行的扩展。 执行用户模式或内核模式调试在 Microsoft Windows 上时，可以使用这些调试器扩展。

### <a name="span-iddebuggerenginespanspan-iddebuggerenginespandebugger-engine"></a><span id="debugger_engine"></span><span id="DEBUGGER_ENGINE"></span>调试器引擎

调试器引擎提供了用于检查和操作在用户模式和内核模式在 Microsoft Windows 上的调试目标的接口。

调试器引擎可以获取目标、 设置断点、 监视事件、 查询符号、 读写内存，并控制线程和进程在目标中。

调试器引擎可用于编写调试器扩展库和独立应用程序。 此类应用程序*调试器引擎应用程序*。 使用调试器引擎的完整功能的调试器引擎应用程序是*调试器*。 例如，WinDbg、 CDB、 NTSD 和 KD 是调试器;调试器引擎提供了其功能的核心。

调试器引擎 API 指定的标头文件 dbgeng.h 中的原型。

有关详细信息，请参阅[调试器引擎概述](debugger-engine-overview.md)并[使用调试器引擎 API](using-the-debugger-engine-api.md)。

.

### <a name="span-idextensionsspanspan-idextensionsspanextensions"></a><span id="extensions"></span><span id="EXTENSIONS"></span>扩展插件

可以通过编写和生成扩展 DLL 创建你自己的调试命令。 例如，你可能想要编写扩展命令以显示复杂数据结构。

有三种不同类型的调试器扩展 Dll:

-   *DbgEng 扩展 Dll*。 这些基于 dbgeng.h 标头文件中的原型。 此类型的每个 DLL 可能导出 DbgEng 扩展命令。 这些扩展命令使用调试器引擎 API，也可能使用 WdbgExts API。

    有关详细信息，请参阅[编写 DbgEng 扩展](writing-dbgeng-extensions.md)。

-   *EngExtCpp 扩展 Dll*。 这些基于 engextcpp.h 和 dbgeng.h 标头文件中的原型。 此类型的每个 DLL 可能导出 DbgEng 扩展命令。 这些扩展命令使用调试器引擎 API 和 EngExtCpp 扩展框架，并还可以使用 WdbgExts API。

-   *WdbgExts 扩展 Dll*。 这些基于 wdbgexts.h 标头文件中的原型。 此类型的每个 DLL 将导出一个或多个 WdbgExts 扩展命令。 这些扩展命令以独占方式使用 WdbgExts API。 有关详细信息请参阅[编写 WdbgExts 扩展](writing-wdbgexts-extensions.md)。

DbgEng API 可用于创建扩展或独立应用程序。 WdbgExts API 包含调试器引擎 API 的功能的子集，可以仅由扩展使用。

应编译和构建使用 Visual Studio 调试器的所有扩展。

如果执行自定义安装，并选择作为调试工具的 Windows 程序包的一部分安装扩展的代码示例**SDK**组件和所有子组件。 它们可在 sdk 中找到\\示例的 Windows 调试工具安装目录的子目录。

编写新的调试器扩展的最简单方法是研究的示例扩展插件。 每个示例扩展插件包括生成文件和源文件用于生成实用工具。 在示例中表示这两种类型的扩展。

## <a name="span-idanalysisspanspan-idanalysisspanspan-idanalysisspanwriting-custom-analysis-debugger-extensions"></a><span id="Analysis"></span><span id="analysis"></span><span id="ANALYSIS"></span>编写自定义分析调试器扩展


可以扩展的功能[ **！ 分析**](-analyze.md)调试器命令通过编写一个分析的扩展插件。 通过提供分析扩展插件，您可以参与的 bug 检查或特定于组件或应用程序的方式中的异常的分析。 在编写分析扩展插件时，还可以编写描述要插件调用了的情况的元数据文件。 当 **！ 分析**运行时，它查找、 加载和运行相应分析扩展插件。 有关详细信息，请参阅[编写自定义分析调试器扩展](writing-custom-analysis-debugger-extensions.md)

## <a name="span-iddmlspanspan-iddmlspancustomizing-debugger-output-using-dml"></a><span id="DML"></span><span id="dml"></span>自定义调试器使用 DML 的输出


您可以自定义调试器使用 DML 的输出。 有关详细信息请参阅[自定义调试器输出使用 DML](customizing-debugger-output-using-dml.md)。

## <a name="span-idjavascriptspanspan-idjavascriptspanspan-idjavascriptspanusing-javascript-to-extend-the-capabilities-of-the-debugger"></a><span id="JavaScript"></span><span id="javascript"></span><span id="JAVASCRIPT"></span>使用 JavaScript 来扩展调试器的功能


使用 JavaScript 创建脚本，了解调试器对象和扩展和自定义调试器的功能。 JavaScript 提供程序起到调试器的内部对象模型脚本语言。 JavaScript 调试器脚本编写提供程序，允许以 JavaScript 用于调试程序。 有关详细信息，请参阅[JavaScript 调试器脚本](javascript-debugger-scripting.md)。

 

 





