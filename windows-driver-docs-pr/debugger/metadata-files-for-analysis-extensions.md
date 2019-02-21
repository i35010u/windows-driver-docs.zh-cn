---
title: 分析扩展插件的元数据文件
description: 当您编写的分析扩展插件时，还可以编写描述所需插件调用了的情况的元数据文件。
ms.assetid: 13B9B7A5-1D68-49A3-825B-454AC070FCC1
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f859a93a32304c8fc75c3ebf4f101297fa515da0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525157"
---
# <a name="metadata-files-for-analysis-extension-plug-ins"></a>分析扩展插件的元数据文件


当您编写的分析扩展插件时，还可以编写描述所需插件调用了的情况的元数据文件。 当[ **！ 分析**](-analyze.md)调试器命令运行时，它使用元数据文件来确定要加载的插件。

创建具有与你的分析扩展插件和.alz 的扩展相同的名称的元数据文件。 例如，如果您的分析扩展插件名为 MyAnalyzer.dll，元数据文件必须命名为 MyAnalyzer.alz。 作为你的分析扩展插件的相同目录中的元数据文件的位置。

分析扩展插件的元数据文件是 ASCII 文本文件，其中包含键 / 值对。 键和值由空格分隔。 密钥可以具有任何非空白字符。 密钥不区分大小写。

之后的密钥和下面的空白区域，相应的值开始。 一个值可以具有以下形式之一。

-   至行尾字符的任何组。 此窗体适用于不包含任何换行符的值。

    **重要**  行元数据文件中的最后一个值具有此窗体的值，如果必须以换行字符结尾。

     

-   任何一组字符之间大括号 {}。 在窗体适用于包含换行字符的值。

以开头的行\#是一个注释，将被忽略。 注释可以开始仅密钥需要的地方。

元数据文件中，可以使用以下项。

| 键            | 描述                                                                                                                                                                                                                                                                                       |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PluginId       | 字符串--标识该插件。                                                                                                                                                                                                                                                                  |
| DebuggeeClass  | 字符串-可能的值为"内核"和"用户"。 指示，该插件所关注的分析仅内核模式失败或仅用户模式故障。                                                                                                                                     |
| BugCheckCode   | 32 位错误检查代码的指示，该插件所关注的分析这[bug 检查代码](bug-check-code-reference2.md)。 单一元数据文件可以指定多个 bug 检查代码。                                                                                                  |
| ExceptionCode  | 32 位异常代码的指示，该插件所关注的分析这[异常代码](https://go.microsoft.com/fwlink/p?LinkID=282670)。 单一元数据文件可以指定多个异常代码。                                                                                 |
| ExecutableName | 字符串--指示在会话中只对感插件下便是要对其进行分析的进程正在运行的可执行文件。 单一元数据文件可以指定多个可执行文件的名称。                                                                                              |
| ImageName      | 字符串--指示，该插件仅对仅在其中的默认分析会考虑此图像 （dll、 sys 或 exe） 有故障的会话中。 分析已确定哪个映像出现故障后，会调用该插件。 单一元数据文件可以指定多个映像名称。 |
| MaxTagCount    | 整数的自定义的最大数目标记的插件的需求。 自定义标记是不是在 extsfns.h 中定义的标记。                                                                                                                                                                |

 

## <a name="span-idexamplemetadatafilesspanspan-idexamplemetadatafilesspanspan-idexamplemetadatafilesspanexample-metadata-files"></a><span id="Example_Metadata_Files"></span><span id="example_metadata_files"></span><span id="EXAMPLE_METADATA_FILES"></span>示例元数据文件


以下元数据文件描述所关注的分析错误检查代码 0xE2 的插件。 （回想一下，最后一行必须结束换行字符。）

```text
PluginId      MyPlugin
DebuggeeClass Kernel
BugCheckCode  0xE2
```

以下元数据文件描述所关注的分析错误检查的 0x8、 0x9，和 0xA 如果 MyDriver.sys 被视为错误的模块的插件。

```text
PluginId      MyPlugin
DebuggeeClass Kernel
BugCheckCode  0x8
BugCheckCode  0x9
BugCheckCode  0xA
ImageName     MyDriver.sys
```

以下元数据文件描述插件兴趣分析异常代码 0xC0000005，如果 MyApp.exe 是所分析的进程正在运行的可执行文件。 此外，该插件可能会创建多达三个自定义标记。

```text
PluginId        MyPlugin
DebuggeeClass   User
ExceptionCode   0xC0000005
ExecutableName  MyApp.exe
```

调试工具的 Windows 中有一个示例可用来生成一个名为 dbgexts.dll 的调试器扩展模块。 此扩展模块实现多个调试器扩展命令，但它也可以用作分析扩展插件;也就是说，它将导出[  **\_EFN\_分析**](https://msdn.microsoft.com/library/windows/hardware/jj983432)函数。 下面是描述 dbgexts.dll 作为分析扩展插件的元数据文件。

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[分析扩展插件写入扩展 ！ 分析](writing-an-analysis-extension-to-extend--analyze.md)

[**\_EFN\_分析**](https://msdn.microsoft.com/library/windows/hardware/jj983432)

[**!analyze**](-analyze.md)

 

 






