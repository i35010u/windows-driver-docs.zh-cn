---
title: 由驱动程序读取 WIA 项属性
description: 由驱动程序读取 WIA 项属性
ms.assetid: 4e592c62-e8bf-4b25-9c65-5a0079d3a857
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05404be0525ece2288f5a2836952c712c79bcd7b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524498"
---
# <a name="reading-wia-item-properties-by-a-driver"></a>由驱动程序读取 WIA 项属性





WIA 微型驱动程序应始终使用属性在其自己的驱动程序项树中作为基础的当前设置。 应用程序是读取和写入微型驱动程序的项树，因为它不会过期。 WIA 微型驱动程序应使用以下 WIA 服务函数读取其驱动程序项树中的属性。

<a href="" id="wiasreadmultiple"></a>[**wiasReadMultiple**](https://msdn.microsoft.com/library/windows/hardware/ff549300)  
读取所有 WIA 属性类型。 这是使 WIA 驱动程序读取 WIA 项，包括自定义属性的任何属性的常规函数。 它可以用于读取每次调用多个属性。

<a href="" id="wiasreadpropstr"></a>[**wiasReadPropStr**](https://msdn.microsoft.com/library/windows/hardware/ff549341)  
读取 WIA 属性是字符串的 (键入 VT\_BSTR)。

<a href="" id="wiasreadproplong"></a>[**wiasReadPropLong**](https://msdn.microsoft.com/library/windows/hardware/ff549330)  
读取 WIA 属性的 4 字节整数 (键入 VT\_I4)。

<a href="" id="wiasreadpropfloat"></a>[**wiasReadPropFloat**](https://msdn.microsoft.com/library/windows/hardware/ff549320)  
四字节实数读取 WIA 属性 (键入 VT\_R4)。

<a href="" id="wiasreadpropguid"></a>[**wiasReadPropGuid**](https://msdn.microsoft.com/library/windows/hardware/ff549325)  
读取 WIA 属性的 Guid (键入 VT\_CLSID)。

<a href="" id="wiasreadpropbin"></a>[**wiasReadPropBin**](https://msdn.microsoft.com/library/windows/hardware/ff549308)  
无符号字节的字符串读取 WIA 属性 (键入 VT\_向量 |VT\_UI1)。

### <a name="reading-legal-values"></a>读取合法值

WIA item 属性包含定义的容器和访问权限类型的属性。 (有关详细信息，请参阅[将 WIA 属性添加到 WIA 项](adding-wia-properties-to-a-wia-item.md)。)容器类型是 WIA\_PROP\_NONE、 WIA\_PROP\_列表中，并且 WIA\_PROP\_范围。 访问权限是 WIA\_PROP\_读取和 WIA\_PROP\_RW。 在验证期间的现有属性，WIA 微型驱动程序应检查内部更新设置，以确定是否应该会显示有效的值。 WIA 微型驱动程序应使用[ **wiasGetPropertyAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff549257)服务函数来读取其 WIA 属性的当前有效值。

 

 




