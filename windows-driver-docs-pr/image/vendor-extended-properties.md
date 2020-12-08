---
title: 供应商扩展的属性
description: 供应商扩展的属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21942a8fc77b6371d096b5564b96527c2ab18c44
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840703"
---
# <a name="vendor-extended-properties"></a>供应商扩展的属性





" **DeviceData** INF 文件" 部分中的 **PropCode** 条目 (参阅供应商 [扩展功能](vendor-extended-features.md)) 中的示例列出了所有供应商扩展的属性代码，用逗号分隔。 对于每个属性代码，都必须存在 **PropCode**_XXXX_ 形式的条目，其中 XXXX 是大写十六进制形式的代码值。 该条目应列出 WIA 属性代码和文本说明 (不需要将其本地化) 括在引号中。

WIA 属性代码应介于0x9802 和0x11802 之间，这是为供应商定义的 WIA 设备属性定义的范围。 可以通过 Microsoft Windows SDK 文档中所述的 **IWiaPropertyStorage：： GetPropertyStream** 和 **IWiaPropertyStorage：： SetPropertyStream** 方法来访问这些属性。

 

 




