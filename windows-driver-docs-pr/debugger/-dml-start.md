---
title: .dml_start（显示 DML 起点）
description: .Dml_start 命令显示的输出可作为使用支持调试器标记语言 (DML) 的命令进行探索的起点。
keywords:
- .dml_start (显示) Windows 调试的 DML 起点
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dml_start (Display DML Starting Point)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cc07897f21785fc3c6e2e691896e4a6331e64b36
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805871"
---
# <a name="dml_start-display-dml-starting-point"></a>dml \_ 开始 (显示 Dml 起始点) 


**Dml \_ start** 命令显示的输出可作为使用支持 [调试器标记语言](debugger-markup-language-commands.md) (dml) 的命令浏览开始的起点。

```dbgcmd
.dml_start
.dml_start filename
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="filename"></span><span id="FILENAME"></span>*名字*  
要显示为起始输出的 DML 文件的名称。

## <a name="span-idusing_the_default_starting_outputspanspan-idusing_the_default_starting_outputspanspan-idusing_the_default_starting_outputspanusing-the-default-starting-output"></a><span id="Using_the_Default_Starting_Output"></span><span id="using_the_default_starting_output"></span><span id="USING_THE_DEFAULT_STARTING_OUTPUT"></span>使用默认起始输出


如果省略 *filename* ，则调试器会按下图所示显示默认的 DML 启动输出。

![dml 开始输出的屏幕截图 \-](images/dmlstart01.png)

上述示例中的每个输出行都是一个链接，单击该链接可以调用其他命令。

## <a name="span-idproviding_a_dml_filespanspan-idproviding_a_dml_filespanspan-idproviding_a_dml_filespanproviding-a-dml-file"></a><span id="Providing_a_DML_File"></span><span id="providing_a_dml_file"></span><span id="PROVIDING_A_DML_FILE"></span>提供 DML 文件


如果提供 DML 文件的路径，该文件将用作起始输出。 例如，假设文件 c： \\MyFavoriteCommands.txt 包含以下文本和 DML 标记。

```dbgcmd
Display all device nodes.
   <link cmd="!devnode 0 1">!devnode 0 1</link>

Display all device nodes that are driven by a specified service.
Include child nodes in the display.
   <b>!devnode 0 1</b> <i>ServiceName</i>  
   Example: <link cmd="!devnode 0 1 usbehci">!devnode 0 1 usbehci</link>

Explore device stacks, device objects, and driver objects.
   <b>!devstack</b>  List the device objects in a device stack.
   <b>!devobj</b>    Display information about a device object.
   <b>!drvobj</b>    Display information about a driver object.
```

命令 **dml \_ 开始 c： \\MyFavoriteCommands.txt** 将显示该文件，如下图所示。

![dml 文件输出的屏幕截图](images/dmlstart02.png)

<a name="remarks"></a>备注
-------

有关可以在 DML 文件中使用的 DML 标记的信息，请参阅适用于 Windows 调试工具的安装文件夹中的 dml.doc。

DML 输出通常适用于 [命令浏览器窗口](command-browser-window.md)。 若要在命令浏览器窗口中显示 DML 文件，请使用 **. browse \_ 。** *filename*

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[调试器标记语言命令](debugger-markup-language-commands.md)

[**。浏览**](-browse--display-command-in-browser-.md)

 

 






