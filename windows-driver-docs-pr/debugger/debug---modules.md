---
title: 调试模块
description: 调试模块
keywords:
- 调试模块
- 可执行文件和路径，调试模块
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0edb51493571bd8289d4f6caab732402eba1f74e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830273"
---
# <a name="debug--modules"></a>调试 | 模块


## <span id="ddk_debug_modules_dbg"></span><span id="DDK_DEBUG_MODULES_DBG"></span>


单击 "**调试**" 菜单上的 "**模块**" 以显示已加载模块的当前列表。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 " **模块**" 时，将显示 " **模块列表** " 对话框。 此对话框列出当前加载到内存中的所有模块。

**模块列表** 分为以下几列：

-   " **名称** " 列指定模块名称。

-   " **开始** " 和 " **结束** " 列指定模块的内存映像的第一个和最后一个地址。

-   **Timestamp** 列指定模块的生成日期和时间。

-   **Checksum** 列指定校验和值。

-   " **符号** " 列显示此模块使用的符号的相关信息。 有关此列中显示的值的详细信息，请参阅 [符号状态缩写](symbol-status-abbreviations.md)。

-   **符号文件** 列指定关联符号文件的路径和文件名。 如果调试器不知道任何符号文件，则将提供可执行文件的名称。

如果单击列的标题栏，则将按该列中的数据对显示进行排序。 如果再次单击标题栏，排序顺序将反转。

如果选择一行，然后单击 " **重新加载**"，则会重新加载该模块的符号信息。

如果选择一行，然后按 CTRL + C，则会将整行复制到剪贴板。

单击 " **关闭** " 以关闭此对话框。

 

 





