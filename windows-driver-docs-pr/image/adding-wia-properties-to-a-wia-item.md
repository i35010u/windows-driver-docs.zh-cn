---
title: 将 WIA 属性添加到 WIA 项
description: 将 WIA 属性添加到 WIA 项
ms.assetid: 0cf4748f-c50a-4781-8b8d-3fb73e5d7242
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b4265ef8fbf1fa24ab94200802f773d9ea57b8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840903"
---
# <a name="adding-wia-properties-to-a-wia-item"></a>将 WIA 属性添加到 WIA 项





每个 WIA 项都包含 WIA 属性。 应用程序读取和写入 WIA 项属性以配置 WIA 微型驱动程序。 WIA 服务为应用程序访问的每个项调用[**IWiaMiniDrv：:D rvinititemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)方法，以便初始化该 WIA 微型驱动程序项的属性。 如果应用程序不读取或写入项的 WIA 属性，则不会为该项调用此方法。 *PWiasContext*参数指向的项上下文指示将用 WIA 属性初始化哪一项。

**IWiaMiniDrv：:D rvinititemproperties**方法应执行以下任务：

1.  使用*pWiasContext*参数中接收的数据确定项类型。 WIA 微型驱动程序可以通过调用[**wiasGetDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetdrvitem)获取[IWiaDrvItem COM 接口](iwiadrvitem-com-interface.md)。 获取此接口后，可以调用[**IWiaDrvItem：： GetItemFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getitemflags)方法来确定 WIA 项类型。

2.  创建一个属性名称和属性 Id 的数组，用于描述在当前项上所需的完整属性集。 创建这些数组后，WIA 微型驱动程序应调用[**wiasSetItemPropNames**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetitempropnames)服务函数。 此函数指示 WIA 服务基于创建的数组生成 WIA 属性集。 应始终在[**wiasWriteMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple)和[**wiasSetItemPropAttribs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetitempropattribs)之前调用此函数。

3.  将初始或默认值设置为新创建的 WIA 属性集。 WIA 微型驱动程序应调用**wiasWriteMultiple**服务函数来设置初始值。 应始终在**wiasSetItemPropAttribs**之前调用此函数。

4.  为每个属性写入有效值和访问权限。 WIA 微型驱动程序应调用**wiasSetItemPropAttribs**服务函数来设置访问权限和有效值。

**请注意**   应用程序负责读取（和重新读取）它们所依赖的任何属性，从而允许应用程序捕获属性值中的任何更改。
扫描仪和照相机具有一组必需的属性。 "[关于 WIA 属性](about-wia-properties.md)" 中列出了这些属性。

有些属性依赖于其他属性。 例如， [**format**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)属性依赖于[**tymed**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)属性。 [WIA 属性](https://docs.microsoft.com/windows-hardware/drivers/image/wia-properties)中介绍了这些属性间依赖关系。

 

 

 




