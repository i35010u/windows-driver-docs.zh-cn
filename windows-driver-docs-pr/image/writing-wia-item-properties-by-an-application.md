---
title: 通过应用程序写入 WIA 项属性
description: 通过应用程序写入 WIA 项属性
ms.assetid: 728f3f73-4815-4d79-ac02-227de7ae9bb7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad6910d4ad692fe9ed8dd6b92c804a95a159bb11
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840661"
---
# <a name="writing-wia-item-properties-by-an-application"></a>通过应用程序写入 WIA 项属性





当 WIA 应用程序写入 WIA 属性（并更新存储在属性中的值）时，WIA 服务将为 WIA 微型驱动程序提供通过调用[**IWiaMiniDrv：:D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)方法来验证传入值的机会。 WIA 微型驱动程序通过在其自身的驱动程序项树中读取属性，将传入值与任何当前值进行比较。 WIA 服务库提供用于访问这些值的函数。

**IWiaMiniDrv：:D rvvalidateitemproperties**方法应执行以下任务：

1.  确定项类型。

2.  确定是否应对传入的 WIA 属性执行任何特殊验证。 若要确定正在编写哪些 WIA 属性，WIA 微型驱动程序可以使用 PROPSPEC 结构的数组（Microsoft Windows SDK 文档中介绍了 PROPSPEC 结构）。 建议 WIA 微型驱动程序在处理 PROPSPEC 数组之前确定项类型，以减少每个 IWiaMiniDrv 上的数组遍历数组的需要 **：:D rvvalidateitemproperties**调用。 如果没有特殊验证要求，或者需要更新设备根项的依赖属性，则只会处理对子项目属性的写入请求。

3.  创建 WIA 属性上下文以访问在 WIA 属性验证期间更改的值，这是更新 WIA 项的依赖属性所必需的。 使用[**wiasCreatePropContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext)和 **wiasGetChangedValue * * * Xxx*服务函数。

4.  使用 WIA 服务函数[**wiasWriteMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple)或 **wiasWriteProp * * ** 更新依赖属性，其中包括更新可能因设置属性而发生更改的所有有效值。 例如，如果 WIA 微型驱动程序支持设置[**wia\_IPA\_DEPTH**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)属性，则当应用程序更改[**wia\_IPA\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)属性时，必须更新位深度的有效列表。

    当[**wia\_IPA\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)属性的值从 WIA\_DATA\_阈值更改为 WIA\_数据\_颜色时，相关的 WIA\_IPA\_DEPTH 属性从报表一位颜色更改深度，到报告24位或48位。

5.  调用[**wiasValidateItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasvalidateitemproperties)服务函数以允许 WIA 服务验证所有其他属性请求。 这是一个 "全部捕获" 案例;WIA 服务具有内置属性验证。

 

 




