---
title: 使用 EnumOptions
description: 使用 EnumOptions
ms.assetid: 6ce16d28-eff7-4701-a592-046f364cda44
keywords:
- EnumOptions
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ce4ebc7f2eb92905d5577525c3baf4a19654bf1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524227"
---
# <a name="using-enumoptions"></a>使用 EnumOptions





可以使用调用方**EnumOptions**检索支持的驱动程序功能和任何 PPD 功能的选项的关键字列表。 PPD 功能**EnumOptions**始终受支持，并返回 PPD.定义的选项

有关驱动程序功能， **EnumOptions**仅支持当前受支持，具有一组固定的选项的功能。 例如: %addeuro 有两个选项："True"和"False"，以及 %pageorder 具有两个选项"FrontToBack"和"BackToFront"。 **EnumOptions** %addeuro （如果语言级别为 2 和更高版本） 支持，如为 %pageorder （如果已启用后台处理程序 EMF 后台处理）。 但如 %CustomPageSize、 %psmemory，以及其他功能具有无限的数量的可能的选项，这意味着**EnumOptions**不支持它们。

当前不支持的驱动程序功能或支持的驱动程序功能不是可通过枚举**EnumOptions**， **EnumOptions**返回 E\_NOTIMPL。

此外，在某些情况下可能不支持驱动程序功能的一些选项。 例如，如果在 Windows 2000 和更高版本的操作系统版本中，然后选择"手册"选项禁用后台处理程序 EMF 后台处理不支持 %pagepersheet 功能。 另举一例，如果打印机不具有 Type42 光栅器，然后"NativeTrueType"不支持选项 %ttdownloadformat。 这些不受支持的选项不会出现在 EnumOptions 输出关键字列表。

Pscript 以特殊方式处理以下功能关键字：

-   \*CustomPageSize 功能关键字将转换为的一个选项\*PageSize 功能关键字，使用"CustomPageSize"所选项关键字。 调用**GetOptionAttribute**来获取其 PPD 参数。

-   \*ManualFeed True 项转换为的一个选项\*InputSlot 功能关键字，使用"ManualFeed"所选项关键字名称。

-   有关\*InputSlot 功能关键字，Pscript 始终添加驱动程序生成的选项与选项关键字名称"\*UseFormTrayTable"作为第一个选项 ("\*"中使用前缀选项关键字名称以避免可能的名称冲突 PPD 定义选项） 后, 跟 PPD.中定义的选项 如果"\*UseFormTrayTable"选择选项后，Pscript 将使用的送纸器格式分配表来自动选择支持选定的纸张大小的送纸器。

 

 




