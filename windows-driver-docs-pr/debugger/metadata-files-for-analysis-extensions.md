---
title: 分析扩展插件的元数据文件
description: 编写分析扩展插件时，还需要编写一个元数据文件，用于描述要调用插件的情况。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e40da85caabf99b2a5412b14e5f0854dbb3d8901
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814529"
---
# <a name="metadata-files-for-analysis-extension-plug-ins"></a>分析扩展插件的元数据文件


编写分析扩展插件时，还需要编写一个元数据文件，用于描述要调用插件的情况。 当 [**！分析**](-analyze.md) 调试器命令运行时，它会使用元数据文件来确定要加载的插件。

创建一个与分析扩展插件同名的元数据文件，并创建 alz 扩展名。 例如，如果 analysis extension 插件的名称为 MyAnalyzer.dll，则必须将元数据文件命名为 MyAnalyzer. alz。 将元数据文件放在与 analysis extension 插件相同的目录中。

Analysis extension 插件的元数据文件是包含键值对的 ASCII 文本文件。 键和值由空格分隔。 键可以有任何非空白字符。 项不区分大小写。

在键和以下空格之后，将开始相应的值。 值可以具有以下格式之一。

-   行末尾的任何字符集。 此窗体适用于不包含任何换行符的值。

    **重要提示**  如果元数据文件中的最后一个值具有此格式的值，则行必须以换行符结尾。

     

-   大括号 {} 之间的任何字符集。 此窗体适用于包含换行符的值。

以开头的行 \# 是注释，将被忽略。 注释只能开始需要键的位置。

可以在元数据文件中使用以下键。

| 键            | 描述                                                                                                                                                                                                                                                                                       |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PluginId       | String-标识插件。                                                                                                                                                                                                                                                                  |
| DebuggeeClass  | 字符串可能的值为 "内核" 和 "用户"。 指示插件仅对分析内核模式故障或仅用户模式故障进行分析感兴趣。                                                                                                                                     |
| BugCheckCode   | 32位 bug 检查代码-指示插件对分析此 [bug 检查代码](bug-check-code-reference2.md)感兴趣。 单个元数据文件可以指定多个 bug 检查代码。                                                                                                  |
| ExceptionCode  | 32位异常代码-指示插件对分析此 [异常代码](/windows/win32/debug/structured-exception-handling)感兴趣。 单个元数据文件可以指定多个异常代码。                                                                                 |
| ExecutableName | String-指示插件仅对这是要分析的进程的运行可执行文件的会话感兴趣。 单个元数据文件可以指定多个可执行名称。                                                                                              |
| ImageName      | String-指示插件仅对默认分析认为此映像 (dll、sys 或 exe) 处于错误状态的会话相关。 此插件是在分析确定哪个映像出错后调用的。 单个元数据文件可以指定多个映像名称。 |
| MaxTagCount    | Integer-插件所需的自定义标记的最大数目。 自定义标记是 extsfns 中定义的标记。                                                                                                                                                                |

 

## <a name="span-idexample_metadata_filesspanspan-idexample_metadata_filesspanspan-idexample_metadata_filesspanexample-metadata-files"></a><span id="Example_Metadata_Files"></span><span id="example_metadata_files"></span><span id="EXAMPLE_METADATA_FILES"></span>示例元数据文件


下面的元数据文件描述了对分析 bug 检查代码0xE2 感兴趣的插件。  (回忆，最后一行必须以换行符结束。 ) 

```text
PluginId      MyPlugin
DebuggeeClass Kernel
BugCheckCode  0xE2
```

下面的元数据文件描述了对分析 bug 检查0x8、0x9 和0xA 感兴趣的插件，前提是将 MyDriver.sys 视为错误的模块。

```text
PluginId      MyPlugin
DebuggeeClass Kernel
BugCheckCode  0x8
BugCheckCode  0x9
BugCheckCode  0xA
ImageName     MyDriver.sys
```

下面的元数据文件描述了对分析异常代码0xC0000005 感兴趣的插件（如果 MyApp.exe 是正在分析的进程的运行可执行文件）。 此外，该插件最多可创建三个自定义标记。

```text
PluginId        MyPlugin
DebuggeeClass   User
ExceptionCode   0xC0000005
ExecutableName  MyApp.exe
```

适用于 Windows 的调试工具提供了一个示例，可用于生成名为 dbgexts.dll 的调试器扩展模块。 此扩展模块实现了几个调试器扩展命令，但它还可以充当分析扩展插件;也就是说，它将导出 [**\_ EFN \_ 分析**](/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)函数。 下面是一个元数据文件，用于将 dbgexts.dll 描述为分析扩展插件。

```text
PluginId         PluginSample
DebuggeeClass   User
ExceptionCode   0xc0000005
ExecutableName      cdb.exe
ExecutableName      windbg.exe
#
# Custom tag descriptions 
#
TagDesc         0xA0000000  SAMPLE_PLUGIN_DEBUG_TEXT    {Sample debug
help text from plug-in analysis}
#
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[编写分析扩展插件以扩展 !analyze](writing-an-analysis-extension-to-extend--analyze.md)

[**\_EFN \_ 分析**](/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)

[**！分析**](-analyze.md)

 

