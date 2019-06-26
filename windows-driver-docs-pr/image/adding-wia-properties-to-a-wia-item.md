---
title: 将 WIA 属性添加到 WIA 项
description: 将 WIA 属性添加到 WIA 项
ms.assetid: 0cf4748f-c50a-4781-8b8d-3fb73e5d7242
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cc5d8162de9598adc6c9ee286763a79e680eb6f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383386"
---
# <a name="adding-wia-properties-to-a-wia-item"></a>将 WIA 属性添加到 WIA 项





每个 WIA 项包含 WIA 属性。 应用程序读取和写入 WIA 项属性，若要配置 WIA 微型驱动程序。 WIA 服务调用[ **IWiaMiniDrv::drvInitItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)方法一次的每个应用程序访问，以初始化该 WIA 微型驱动程序项目的属性的项。 如果应用程序不读取或写入 WIA 属性在某项目上该项不调用此方法。 项目上下文的*pWiasContext*参数指向指示哪一项将使用 WIA 属性进行初始化。

**IWiaMiniDrv::drvInitItemProperties**方法应执行以下任务：

1.  使用中收到的数据*pWiasContext*参数，以确定的项类型。 WIA 微型驱动程序可以获取[IWiaDrvItem COM 接口](iwiadrvitem-com-interface.md)通过调用[ **wiasGetDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetdrvitem)。 获取此接口之后, [ **IWiaDrvItem::GetItemFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getitemflags)方法可以调用以确定 WIA 项类型。

2.  创建的属性名称和描述完整的属性的当前项上设置所需的属性 Id 的数组。 在创建后这些阵列，WIA 微型驱动程序应调用[ **wiasSetItemPropNames** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetitempropnames)服务函数。 此函数指示 WIA 服务来构建基于创建数组的 WIA 属性集。 应始终调用此函数之前[ **wiasWriteMultiple** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritemultiple)并[ **wiasSetItemPropAttribs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetitempropattribs)。

3.  设置到新创建的 WIA 属性写入初始或默认情况下，设置值。 WIA 微型驱动程序应调用**wiasWriteMultiple**服务函数设置初始值。 应始终调用此函数之前**wiasSetItemPropAttribs**。

4.  编写有效的值，并为每个属性访问权限。 WIA 微型驱动程序应调用**wiasSetItemPropAttribs**服务函数设置的访问权限和有效的值。

**请注意**  应用程序负责读取 （和重新读取），它们依赖于，从而允许应用程序来捕获中的属性值的任何更改的任何属性。
扫描仪和照相机具有所需属性的一组。 中列出了这些属性[关于 WIA 属性](about-wia-properties.md)。

某些属性在其他属性上有依赖关系。 例如， [**格式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)属性是依赖于[ **tymed** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)属性。 中介绍了这些属性间的依赖关系[WIA 属性](https://docs.microsoft.com/windows-hardware/drivers/image/wia-properties)。

 

 

 




