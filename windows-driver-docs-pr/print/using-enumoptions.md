---
title: 使用 EnumOptions
description: 使用 EnumOptions
keywords:
- EnumOptions
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8f62dcc80add80a307f53e9e79579b695ec4771
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835443"
---
# <a name="using-enumoptions"></a>使用 EnumOptions





调用方可以使用 **EnumOptions** 检索支持的驱动程序功能和任何 PPD 功能选项的关键字列表。 对于 PPD 功能，始终支持 **EnumOptions** ，并返回由 PPD 定义的选项。

对于驱动程序功能， **EnumOptions** 仅支持当前受支持的功能，并且具有一组固定的选项。 例如：% AddEuro 有两个选项： "True" 和 "False"，% PageOrder 有两个选项 "FrontToBack" 和 "BackToFront"。 如果语言级别为2和更) 高，则% AddEuro (支持 **EnumOptions** ，如果 (启用) 了后台处理 EMF 假脱机，则为% PageOrder。 但某些功能（例如% CustomPageSize、% PSMemory）和其他功能具有无限数量的可能选项，这意味着不支持 **EnumOptions** 。

对于当前不支持的驱动程序功能，或对于不可通过 **EnumOptions** 枚举的受支持驱动程序功能， **EnumOptions** 将返回 E \_ NOTIMPL。

此外，某些情况下可能不支持驱动程序功能的某些选项。 例如，如果在 Windows 2000 和更高版本的操作系统版本上禁用了后台处理程序 EMF 假脱机，则% PagePerSheet 功能不支持 "手册" 选项。 在另一个示例中，如果打印机没有 Type42 光栅，则% TTDownloadFormat 不支持 "NativeTrueType" 选项。 这些不受支持的选项不会显示在 EnumOptions 的 "输出关键字" 列表中。

Pscript 以特殊方式处理以下特征关键字：

-   \*CustomPageSize 功能关键字转换为 \* PageSize 功能关键字的选项，其中 "CustomPageSize" 是 option 关键字。 调用 **GetOptionAttribute** 获取其 PPD 参数。

-   \*ManualFeed True 条目转换为 \* InputSlot feature 关键字的选项，其中 "ManualFeed" 是选项关键字名称。

-   对于 \* InputSlot 功能关键字，Pscript 始终将选项关键字名称为 "UseFormTrayTable" 的驱动程序生成的选项添加 \* 为第一个选项 (在 \* 选项关键字名称中使用 "" 前缀，以避免可能与 ppd 中定义的选项的名称冲突) ，其后是 ppd 中定义的选项。 如果选择了 " \* UseFormTrayTable" 选项，则 Pscript 将使用 "送纸器分配" 表来自动选择支持所选纸张大小的送纸器。

 

 




