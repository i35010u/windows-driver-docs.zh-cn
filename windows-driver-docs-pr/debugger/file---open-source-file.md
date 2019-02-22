---
title: 文件打开源文件
description: 文件打开源文件
ms.assetid: 27007865-7517-40df-a30a-26ecf3cec9f5
keywords:
- 文件打开源文件
- 调试时，文件打开源文件的源
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcd7041e4deceefaec71de6e784c4be9910c7d85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519653"
---
# <a name="file--open-source-file"></a>文件 |开放源代码文件


## <span id="ddk_file_open_source_file_dbg"></span><span id="DDK_FILE_OPEN_SOURCE_FILE_DBG"></span>


单击**打开源文件**上**文件**菜单加载特定的源文件。

此命令相当于按 CTRL + O 或单击**开放源代码文件 (Ctrl + O)** 按钮 (![开放源代码文件按钮的屏幕截图](images/tbopen.png))。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

当您单击**打开源文件**，则**打开源文件**对话框随即出现。 若要打开一个文件，请执行以下操作：

1.  在中**查找**列表中，选择该文件所在的目录。 默认情况下，选择上一次打开的目录。

2.  在中**类型的文件**列表中，选择你想要打开的文件的类型。 仅使用所选扩展的文件将显示在**打开源文件**对话框。
    **请注意**  还可以使用中的通配符模式**文件名**框，以显示仅具有特定扩展名的文件。 在更改之前的会话中保留新的通配符模式。 可以使用通配符模式，之间用分号分隔的任意组合。 例如，输入 **\*。非独占;\*.H;\*.CPP**显示具有这些扩展名的所有文件。 最大的行中的字符数为 251。

     

3.  如果找到该文件所需，双击文件名称，或单击文件名称并单击**打开**。

    -或-

    若要放弃更改并关闭对话框，请单击**取消**。

当你指向时显示在 WinDbg 中最近打开的四个文件的名称**最近使用的文件**上**文件**菜单。 若要打开这些文件之一，请单击其名称。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关源的文件和源路径的详细信息并加载源文件的其他方法，请参阅[源路径](source-path.md)。

 

 





