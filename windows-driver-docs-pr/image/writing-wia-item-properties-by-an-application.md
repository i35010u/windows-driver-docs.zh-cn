---
title: 通过应用程序写入 WIA 项属性
description: 通过应用程序写入 WIA 项属性
ms.assetid: 728f3f73-4815-4d79-ac02-227de7ae9bb7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4986a4f06aab19a1e4eb5adfd03c19ec46d078d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365001"
---
# <a name="writing-wia-item-properties-by-an-application"></a>通过应用程序写入 WIA 项属性





WIA 服务时将写入到 WIA 属性 WIA 应用程序 （和更新属性中存储的值），使 WIA 微型驱动程序有机会来验证传入值通过调用[ **IWiaMiniDrv::drvValidateItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)方法。 WIA 微型驱动程序将为任何当前的值的传入值通过读取其自己的驱动程序项树中的属性进行比较。 WIA 服务库提供用于访问这些值的函数。

**IWiaMiniDrv::drvValidateItemProperties**方法应执行以下任务：

1.  确定项类型。

2.  确定是否应传入的 WIA 属性执行任何特殊的验证。 若要确定哪些 WIA 属性写入，WIA 微型驱动程序可以使用 PROPSPEC 结构 （Microsoft Windows SDK 文档中描述了 PROPSPEC 结构） 的数组。 建议 WIA 微型驱动程序确定的项类型，然后再处理 PROPSPEC 数组来降低需要遍历数组上每个**IWiaMiniDrv::drvValidateItemProperties**调用。 如果没有特殊的验证要求，或如果需要更新设备的根项的依赖属性，只有写请求到子项目属性将会处理。

3.  创建 WIA 属性上下文来访问更改 WIA 属性在验证期间，需要更新 WIA 项的依赖属性的值。 使用[ **wiasCreatePropContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatepropcontext)和 **wiasGetChangedValue * * * Xxx*服务函数。

4.  更新使用 WIA 服务函数的依赖属性[ **wiasWriteMultiple** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritemultiple)或 **wiasWriteProp * * * Xxx*，其中包括更新任何可能的有效值由于属性设置已更改。 例如，如果你 WIA 微型驱动程序支持设置[ **WIA\_IPA\_深度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)属性，您必须位深度的有效列表应用程序发生更改时更新[**WIA\_IPA\_数据类型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)属性。

    时的值[ **WIA\_IPA\_数据类型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)属性更改从 WIA\_数据\_WIA 的阈值\_数据\_颜色、 相关的 WIA\_IPA\_DEPTH 属性将更改从报表到报告 24 位或 48 位的一位颜色深度。

5.  调用[ **wiasValidateItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasvalidateitemproperties)服务函数来让 WIA 服务验证所有其他属性的请求。 这是一种"全部捕捉"情况;WIA 服务都有内置属性验证。

 

 




