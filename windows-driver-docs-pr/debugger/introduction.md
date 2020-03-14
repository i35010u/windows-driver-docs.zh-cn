---
title: 调试器引擎简介
description: 调试器引擎简介
ms.assetid: fa52a1f0-9397-48a5-acbd-ce5347c0baef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8f9de13e52cd6f5d717ccf9ad814df259eac7a0
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242812"
---
# <a name="debugger-engine-introduction"></a>调试器引擎简介

此文档介绍如何使用调试器引擎，以及如何编写将在 WinDbg、KD、CDB 和 NTSD 中运行的扩展。 在 Microsoft Windows 上执行用户模式或内核模式调试时，可以使用这些调试器扩展。

### <a name="span-iddebugger-enginespandebugger-engine"></a><span id="debugger-engine"></span>调试器引擎

调试器引擎提供了一个接口，用于检查和操作 Microsoft Windows 上用户模式和内核模式下的调试目标。

调试器引擎可以获取目标、设置断点、监视事件、查询符号、读取和写入内存，以及控制目标中的线程和进程。

您可以使用调试器引擎来编写调试器扩展库和独立应用程序。 此类应用程序是*调试器引擎应用*程序。 使用调试器引擎全部功能的调试器引擎应用程序是一个*调试器*。 例如，WinDbg、CDB、NTSD 和 KD 都是调试器;调试器引擎提供其功能的核心。

调试器引擎 API 由头文件 dbgeng 中的原型指定。

### <a name="incomplete-documentation"></a>文档不完整

这是一个初步文档，当前不完整。

对于很多与调试器和调试器引擎相关的概念，此处未介绍这些概念，请参阅本文档的[调试技术](debugging-techniques.md)部分。

若要获取调试器引擎 API 的一些当前未记录的功能，请使用[**execute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-execute)方法执行单个调试器命令。

### <a name="span-idextensionsspanspan-idextensionsspanextensions"></a><span id="extensions"></span><span id="EXTENSIONS"></span>扩展名

可以通过编写和生成扩展 DLL 来创建自己的调试命令。 例如，您可能希望编写一个扩展命令以显示复杂的数据结构。

有三种不同类型的调试器扩展 Dll：

-   *DbgEng 扩展 dll*。 它们基于 dbgeng 头文件中的原型。 此类型的每个 DLL 都可以导出 DbgEng extension 命令。 这些扩展命令使用调试器引擎 API，还可以使用 WdbgExts API。

-   *EngExtCpp 扩展 dll*。 它们基于 engextcpp 和 dbgeng 标头文件中的原型。 此类型的每个 DLL 都可以导出 DbgEng extension 命令。 这些扩展命令同时使用调试器引擎 API 和 EngExtCpp 扩展框架，还可以使用 WdbgExts API。

-   *WdbgExts 扩展 dll*。 它们基于 wdbgexts 头文件中的原型。 此类型的每个 DLL 都导出一个或多个 WdbgExts 扩展命令。 这些扩展命令仅使用 WdbgExts API。

DbgEng API 可用于创建扩展或独立应用程序。 WdbgExts API 包含调试器引擎 API 的一部分功能，只能由扩展使用。

所有调试器扩展都应使用生成实用工具进行编译和生成。 构建实用程序包含在 Windows 驱动程序工具包（WDK）中。

如果执行自定义安装并选择**SDK**组件及其所有子组件，则扩展代码示例将作为 Windows 程序包的调试工具的一部分进行安装。 可在适用于 Windows 的调试工具 "安装目录" 的 sdk\\示例 "子目录中找到它们。

编写新调试器扩展的最简单方法是学习示例扩展。 每个示例扩展都包含用于生成实用工具的生成文件和源文件。 示例中表示这两种类型的扩展。

## <a name="span-idwriting_custom_analysis_debugger_extensionsspanspan-idwriting_custom_analysis_debugger_extensionsspanspan-idwriting_custom_analysis_debugger_extensionsspanwriting-custom-analysis-debugger-extensions"></a><span id="Writing_Custom_Analysis_Debugger_Extensions"></span><span id="writing_custom_analysis_debugger_extensions"></span><span id="WRITING_CUSTOM_ANALYSIS_DEBUGGER_EXTENSIONS"></span>编写自定义分析调试器扩展


可以通过编写分析扩展插件来扩展[ **！分析**](-analyze.md)调试器命令的功能。 通过提供分析扩展插件，您可以以特定于您自己的组件或应用程序的方式参与对 bug 检查或异常的分析。 编写分析扩展插件时，还需要编写一个元数据文件，用于描述要为其调用插件的情况。 当 **！分析**运行时，它会查找、加载和运行相应的分析扩展插件。 有关详细信息，请参阅[编写自定义分析调试器扩展](writing-custom-analysis-debugger-extensions.md)

## <a name="span-idcustomizing_debugger_output_using_dmlspanspan-idcustomizing_debugger_output_using_dmlspanspan-idcustomizing_debugger_output_using_dmlspancustomizing-debugger-output-using-dml"></a><span id="Customizing_Debugger_Output_Using_DML"></span><span id="customizing_debugger_output_using_dml"></span><span id="CUSTOMIZING_DEBUGGER_OUTPUT_USING_DML"></span>使用 DML 自定义调试器输出


您可以使用 DML 自定义调试器输出。 有关详细信息，请参阅[使用 DML 自定义调试器输出](customizing-debugger-output-using-dml.md)。

## <a name="span-idjavascriptspanspan-idjavascriptspanspan-idjavascriptspanusing-javascript-to-extend-the-capabilities-of-the-debugger"></a><span id="JavaScript"></span><span id="javascript"></span><span id="JAVASCRIPT"></span>使用 JavaScript 扩展调试器的功能


使用 JavaScript 创建脚本，这些脚本可理解调试器对象并扩展和自定义调试器的功能。 JavaScript 提供程序将脚本语言桥接到调试器的内部对象模型中。 JavaScript 调试器脚本提供程序允许将 JavaScript 用于调试器。 有关详细信息，请参阅[JavaScript 调试器脚本](javascript-debugger-scripting.md)。

 

 





