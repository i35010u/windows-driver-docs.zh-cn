---
title: 文件打开源文件
description: 文件打开源文件
ms.assetid: 27007865-7517-40df-a30a-26ecf3cec9f5
keywords:
- 文件打开源文件
- 源调试，文件打开源文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcd7041e4deceefaec71de6e784c4be9910c7d85
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323603"
---
# <a name="file--open-source-file"></a>文件 | 打开源文件


## <span id="ddk_file_open_source_file_dbg"></span><span id="DDK_FILE_OPEN_SOURCE_FILE_DBG"></span>


单击 "**文件**" 菜单上的 "**打开源文件**" 以加载特定的源文件。

此命令等效于按 CTRL + O 或单击 "打开源文件" **（CTRL + o）** 按钮（![screen ](images/tbopen.png) 的 "打开源文件" 按钮的快照。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 "**打开源文件**" 时，将显示 "**打开源文件**" 对话框。 若要打开文件，请执行以下操作：

1.  在 "**查找范围**" 列表中，选择该文件所在的目录。 默认情况下，选择上一次打开的目录。

2.  在 "**文件类型**" 列表中，选择要打开的文件的类型。 "**打开源文件**" 对话框中只显示具有所选扩展名的文件。
    **请注意**  You 还可以**在 "文件名" 框**中使用通配符模式，以便仅显示具有特定扩展名的文件。 新的通配符模式将保留在会话中，直到你进行更改。 你可以使用通配符模式的任意组合，用分号分隔。 例如，输入 **\*。 \* .H; \*** 将显示具有这些扩展名的所有文件。 行中的最大字符数为251。

     

3.  如果找到所需的文件，请双击该文件名，或单击文件名，然后单击 "**打开**"。

    -或-

    若要放弃更改并关闭对话框，请单击 "**取消**"。

当你指向 "**文件**" 菜单上的 "**最近使用的文件**" 时，将显示在 WinDbg 最近打开的四个文件的名称。 若要打开这些文件中的一个，请单击其名称。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关源文件和源路径以及其他加载源文件的方式的详细信息，请参阅[源路径](source-path.md)。

 

 





