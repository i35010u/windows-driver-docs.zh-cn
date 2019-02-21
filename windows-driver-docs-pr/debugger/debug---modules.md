---
title: 调试模块
description: 调试模块
ms.assetid: 4107ff36-31c4-45a6-95f6-b647543f01be
keywords:
- 调试模块
- 可执行文件和路径，调试模块
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80a1d251f6d5f9edc95f2ffaf21f05219e4ba9c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546367"
---
# <a name="debug--modules"></a>调试 |模块


## <span id="ddk_debug_modules_dbg"></span><span id="DDK_DEBUG_MODULES_DBG"></span>


单击**模块**上**调试**菜单可显示的当前列表加载的模块。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

当您单击**模块**，则**模块列表**对话框随即出现。 此对话框列出了当前加载到内存中的所有模块。

**模块列表**分为以下各列：

-   **名称**列指定的模块名称。

-   **启动**并**最终**列指定模块的内存中的映像的第一个和最后一个地址。

-   **时间戳**列指定的生成日期和时间的模块。

-   **校验和**列指定的校验和值。

-   **符号**列将显示此模块使用的符号信息。 此列中显示的值的详细信息，请参阅[符号状态缩写](symbol-status-abbreviations.md)。

-   **符号文件**列指定关联的符号文件的路径和文件。 如果调试器不知道的任何符号文件，而是提供可执行文件的名称。

如果单击某一列的标题栏，显示将按该列中数据进行排序。 如果单击标题栏中再次，反转排序顺序。

如果您选择某一行，然后单击**重新加载**，将重新加载模块的符号信息。

如果选择一个行，按 CTRL + C，整行复制到剪贴板。

单击**关闭**以关闭此对话框。

 

 





