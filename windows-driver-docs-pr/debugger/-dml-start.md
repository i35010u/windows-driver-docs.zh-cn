---
title: .dml_start（显示 DML 起点）
description: .Dml_start 命令显示可作为一个起始点，探索使用支持调试器标记语言 (DML) 命令的输出。
ms.assetid: 1CFCACDC-B253-4E9B-9877-EE9F1E91395F
keywords:
- .dml_start （显示 DML 开始位置） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dml_start (Display DML Starting Point)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a7fae322482beeb1624a1facc33185954cdc5df8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336811"
---
# <a name="dmlstart-display-dml-starting-point"></a>.dml\_启动 （显示 DML 起始点）


**.Dml\_启动**命令显示了探索使用命令支持可作为起始点的输出[调试器标记语言](debugger-markup-language-commands.md)(DML)。

```dbgcmd
.dml_start
.dml_start filename
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="filename"></span><span id="FILENAME"></span>*filename*  
要作为起始输出显示 DML 文件的名称。

## <a name="span-idusingthedefaultstartingoutputspanspan-idusingthedefaultstartingoutputspanspan-idusingthedefaultstartingoutputspanusing-the-default-starting-output"></a><span id="Using_the_Default_Starting_Output"></span><span id="using_the_default_starting_output"></span><span id="USING_THE_DEFAULT_STARTING_OUTPUT"></span>使用默认的启动输出


如果*文件名*是省略，则调试器会显示默认 DML 起始输出如以下图像中所示。

![屏幕截图：.dml\-启动输出](images/dmlstart01.png)

在前面的示例输出的每一行是一个链接，可以单击以调用其他命令。

## <a name="span-idprovidingadmlfilespanspan-idprovidingadmlfilespanspan-idprovidingadmlfilespanproviding-a-dml-file"></a><span id="Providing_a_DML_File"></span><span id="providing_a_dml_file"></span><span id="PROVIDING_A_DML_FILE"></span>提供 DML 文件


如果提供 DML 文件的路径，该文件用作起始输出。 例如，假设文件 c:\\MyFavoriteCommands.txt 包含以下文本和 DML 标记。

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

该命令 **.dml\_启动 c:\\MyFavoriteCommands.txt**将显示该文件，在下图中所示。

![dml 文件输出的屏幕截图](images/dmlstart02.png)

<a name="remarks"></a>备注
-------

有关可以使用 DML 文件中的 DML 标记的信息，请参阅有关 Windows 调试工具的 dml.doc 安装文件夹中的。

DML 输出通常中工作[命令浏览器窗口](command-browser-window.md)。 若要在命令浏览器窗口中显示 DML 文件，请使用 **.browse.dml\_启动** *filename*。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[调试器标记语言命令](debugger-markup-language-commands.md)

[**.browse**](-browse--display-command-in-browser-.md)

 

 






