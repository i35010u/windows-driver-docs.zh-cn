---
title: 文件打开源文件
description: 文件打开源文件
keywords:
- 文件打开源文件
- 源调试，文件打开源文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c80f4f968ae5b33a99e86df210753c03e1bf62c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832525"
---
# <a name="file--open-source-file"></a>文件 | 打开源文件


## <span id="ddk_file_open_source_file_dbg"></span><span id="DDK_FILE_OPEN_SOURCE_FILE_DBG"></span>


单击 "**文件**" 菜单上的 "**打开源文件**" 以加载特定的源文件。

此命令等效于按 CTRL + O 或单击 **打开源文件 (CTRL + o)** 按钮 (![ "打开源文件" 按钮) 的屏幕截图 ](images/tbopen.png) 。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 " **打开源文件**" 时，将显示 " **打开源文件** " 对话框。 若要打开文件，请执行以下操作：

1.  在 " **查找范围** " 列表中，选择该文件所在的目录。 默认情况下，选择上一次打开的目录。

2.  在 " **文件类型** " 列表中，选择要打开的文件的类型。 " **打开源文件** " 对话框中只显示具有所选扩展名的文件。
    **注意**  你还可以 **在 "文件名" 框** 中使用通配符模式，以便仅显示具有特定扩展名的文件。 新的通配符模式将保留在会话中，直到你进行更改。 你可以使用通配符模式的任意组合，用分号分隔。 例如，输入 **\* 。增量\*.高\*.CPP** 显示具有这些扩展名的所有文件。 行中的最大字符数为251。

     

3.  如果找到所需的文件，请双击该文件名，或单击文件名，然后单击 " **打开**"。

    \- 或 -

    若要放弃更改并关闭对话框，请单击 " **取消**"。

当你指向 "**文件**" 菜单上的 "**最近使用的文件**" 时，将显示在 WinDbg 最近打开的四个文件的名称。 若要打开这些文件中的一个，请单击其名称。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关源文件和源路径以及其他加载源文件的方式的详细信息，请参阅 [源路径](source-path.md)。

 

 





