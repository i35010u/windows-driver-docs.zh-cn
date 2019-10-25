---
title: 通过驱动程序读取 WIA 项属性
description: 通过驱动程序读取 WIA 项属性
ms.assetid: 4e592c62-e8bf-4b25-9c65-5a0079d3a857
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7995023f08a606e0844959d99ea696a19a7934c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840763"
---
# <a name="reading-wia-item-properties-by-a-driver"></a>通过驱动程序读取 WIA 项属性





WIA 微型驱动程序应始终使用其自己的驱动程序项树中的属性作为当前设置的基础。 由于应用程序在微型驱动程序的项树中进行读取和写入，因此它永远不会过期。 WIA 微型驱动程序应使用以下 WIA 服务函数从其驱动程序项树中的属性进行读取。

<a href="" id="wiasreadmultiple"></a>[**wiasReadMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadmultiple)  
读取所有 WIA 属性类型。 这是一个常规功能，它允许 WIA 驱动程序读取 WIA 项上存在的任何属性，包括自定义属性。 它可用于读取每个调用的多个属性。

<a href="" id="wiasreadpropstr"></a>[**wiasReadPropStr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropstr)  
读取作为字符串的 WIA 属性（type VT\_BSTR）。

<a href="" id="wiasreadproplong"></a>[**wiasReadPropLong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadproplong)  
读取由四个字节构成的 WIA 属性（VT\_I4）。

<a href="" id="wiasreadpropfloat"></a>[**wiasReadPropFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropfloat)  
读取包含四个字节实数的 WIA 属性（类型 VT\_R4）。

<a href="" id="wiasreadpropguid"></a>[**wiasReadPropGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropguid)  
读取作为 Guid 的 WIA 属性（type VT\_CLSID）。

<a href="" id="wiasreadpropbin"></a>[**wiasReadPropBin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropbin)  
读取作为无符号字节的字符串的 WIA 属性（type VT\_VECTOR |VT\_UI1）。

### <a name="reading-legal-values"></a>读取合法值

WIA 项目属性包含定义容器类型和访问权限的属性。 （有关详细信息，请参阅向[Wia 项添加 Wia 属性](adding-wia-properties-to-a-wia-item.md)。）容器类型为 WIA\_类型\_NONE、WIA\_"\_列表" 和 "WIA\_"\_范围 "。 访问权限是 WIA\_的\_读取和 WIA\_的\_RW。 在现有属性验证过程中，WIA 微型驱动程序应检查内部更新设置，以确定它是否应读取有效值。 WIA 微型驱动程序应使用[**wiasGetPropertyAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetpropertyattributes)服务函数读取其 WIA 属性的当前有效值。

 

 




