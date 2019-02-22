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
ms.openlocfilehash: fddd9d92defca0ae15f3c5e0829206ce7651bba4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555005"
---
# <a name="ppd-features"></a>PPD 功能





中的 PPD 文件内定义 PPD 功能 **\*OpenUI**/**\*CloseUI**结构关键字对和中的处理方式类似某些 PPD 关键字Pscript 驱动程序。 尽管**EnumFeatures**列出了 **\*LeadingEdge**并 **\*UseHWMargins**关键字，它们不定义内 PPD  **\*OpenUI**/**\*CloseUI**结构关键字对。 因此， **GetOptions**并**SetOptions**方法会忽略这些关键字，如果它们出现在功能列表。 PPD 功能/选项关键字是区分大小写。

**SetOptions**以特殊方式处理某些 PPD 功能：

-   如果打印机的 PPD 文件包含 **\*OutputOrder**功能关键字和**SetOptions**调用以更改选项选择此功能，则 **%pageorder**驱动程序功能设置将更改以匹配新的输出顺序。 这样做是为了防止执行不必要的页顺序模拟后台处理程序。

-   如果打印机的 PPD 文件包含 **\*OutputBin**功能关键字和**SetOptions**调用以更改的当前设置的这项功能及更改原因的选项选择 **%pageorder**驱动程序功能以相反的顺序，打印机的页面并 **%metafilespooling**为"False"，则 **%metafilespooling**将重置为"True"。

-   启用后台处理程序 EMF 后台处理，并**逐份打印**设置为"True"(此值可以设置中的公共部分直接[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)结构，或通过调用**SetOptions**上的 PPD **\*逐份打印**功能关键字)，但**逐份打印**功能不是目前不可用，和 **%MetafileSpooling**为"False"，则 **%metafilespooling**将重置为"True"。 这是所有请求中的设置时**SetOptions**应用调用。

-   如果**双工**设置为单工 (这设置可以直接在 DEVMODE 结构的或通过调用的公共部分**SetOptions**上的 PPD **\*双工**功能关键字)，但 **%pagepersheet**设置为"手册"，然后 **%pagepersheet**将更改为"2"。 这是所有请求中的设置时**SetOptions**应用调用。

 

 




