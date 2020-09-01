---
title: 通过驱动程序读取 WIA 项属性
description: 通过驱动程序读取 WIA 项属性
ms.assetid: 4e592c62-e8bf-4b25-9c65-5a0079d3a857
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10cf879521aad3d30ad0d970d6cddeb047df12fc
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187593"
---
# <a name="reading-wia-item-properties-by-a-driver"></a>通过驱动程序读取 WIA 项属性





WIA 微型驱动程序应始终使用其自己的驱动程序项树中的属性作为当前设置的基础。 由于应用程序在微型驱动程序的项树中进行读取和写入，因此它永远不会过期。 WIA 微型驱动程序应使用以下 WIA 服务函数从其驱动程序项树中的属性进行读取。

<a href="" id="wiasreadmultiple"></a>[**wiasReadMultiple**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadmultiple)  
读取所有 WIA 属性类型。 这是一个常规功能，它允许 WIA 驱动程序读取 WIA 项上存在的任何属性，包括自定义属性。 它可用于读取每个调用的多个属性。

<a href="" id="wiasreadpropstr"></a>[**wiasReadPropStr**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropstr)  
读取作为字符串 (类型 VT BSTR) 的 WIA 属性 \_ 。

<a href="" id="wiasreadproplong"></a>[**wiasReadPropLong**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadproplong)  
 (type VT I4) 读取属于四个字节整数的 WIA 属性 \_ 。

<a href="" id="wiasreadpropfloat"></a>[**wiasReadPropFloat**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropfloat)  
 (键入 VT R4) ，读取包含四个字节实数的 WIA 属性 \_ 。

<a href="" id="wiasreadpropguid"></a>[**wiasReadPropGuid**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropguid)  
读取作为 Guid 的 WIA 属性， (type VT \_ CLSID) 。

<a href="" id="wiasreadpropbin"></a>[**wiasReadPropBin**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropbin)  
读取作为无符号字节字符串的 WIA 属性 (类型 VT \_ VECTOR |VT \_ UI1) 。

### <a name="reading-legal-values"></a>读取合法值

WIA 项目属性包含定义容器类型和访问权限的属性。  (获取详细信息，请参阅向 [Wia 项添加 Wia 属性](adding-wia-properties-to-a-wia-item.md)。 ) 容器类型为 wia 属性 \_ \_ NONE、WIA 属性 \_ \_ 列表和 wia 属性 \_ \_ 范围。 访问权限为 WIA 的 \_ " \_ 读取" 和 "wia" \_ \_ 。 在现有属性验证过程中，WIA 微型驱动程序应检查内部更新设置，以确定它是否应读取有效值。 WIA 微型驱动程序应使用 [**wiasGetPropertyAttributes**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetpropertyattributes) 服务函数读取其 WIA 属性的当前有效值。

 

