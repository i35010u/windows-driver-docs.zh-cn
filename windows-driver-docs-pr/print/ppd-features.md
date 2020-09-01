---
title: PPD 功能
description: PPD 功能
ms.assetid: ee78031a-2138-4d0c-ac8a-5328aa54d904
keywords:
- PPD 文件 WDK Pscript
- 非 PPD 功能 WDK Pscript
- 驱动程序功能 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f69ee5ab3ca3813df28a24d909bb79cb76e061d1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209495"
---
# <a name="ppd-features"></a>PPD 功能





Ppd 功能在** \* OpenUI** / ** \* CloseUI**结构关键字对中的 ppd 文件中定义，并在与 Pscript 驱动程序类似的某些 PPD 关键字中定义。 尽管**EnumFeatures**列出了** \* LeadingEdge**和** \* UseHWMargins**关键字，但没有在 PPD ** \* OpenUI** / ** \* CloseUI**结构关键字对中定义它们。 因此，如果这些关键字出现在功能列表中，则 **GetOptions** 和 **SetOptions** 方法将忽略它们。 PPD 功能/选项关键字区分大小写。

**SetOptions** 以特殊方式处理某些 PPD 功能：

-   如果打印机的 PPD 文件包含** \* OutputOrder** feature 关键字，而调用**SetOptions**来更改此功能的选项，则将更改 **% PageOrder**驱动程序功能设置以匹配新的输出顺序。 这样做是为了防止后台处理程序执行不必要的页面顺序模拟。

-   如果打印机的 PPD 文件包含** \* OutputBin** feature 关键字，并调用**SetOptions**来更改此功能的选项，并且更改导致 **% PageOrder**驱动程序功能的当前设置与打印机的页面顺序相反，而 **% MetafileSpooling**为 "False"，则 **% MetafileSpooling**将重置为 "True"。

-   当后台处理程序启用了 EMF 假脱机功能，并且将**collate**设置为 "true" 时 (可以直接在[**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew)结构的公共部分中设置此值，也可以通过对 PPD 的** \* Collate**排序功能) 关键字调用**SetOptions**来进行设置，但**collate**功能当前不可**用，%** **MetafileSpooling**将重置为 "True"。 在应用 **SetOptions** 调用中的所有请求的设置时，将执行此操作。

-   如果将 "**双工**" 设置为 "单工 (则可以直接在 DEVMODE 结构的公共部分中设置此项，也可以通过对 PPD 的** \* 双工**功能关键字) 调用**SetOptions** ，但将 **% PagePerSheet**设置为" 手册 "，然后将 **% PagePerSheet**更改为" 2 "。 在应用 **SetOptions** 调用中的所有请求的设置时，将执行此操作。

 

