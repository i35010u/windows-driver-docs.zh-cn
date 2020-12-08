---
title: 通过应用程序写入 WIA 项属性
description: 通过应用程序写入 WIA 项属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31c3c803c0359ecf1b751df5b8c6160df22780a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826333"
---
# <a name="writing-wia-item-properties-by-an-application"></a>通过应用程序写入 WIA 项属性





当 WIA 应用程序向 WIA 属性写入 (并更新属性) 中存储的值时，WIA 服务将为 WIA 微型驱动程序提供通过调用 [**IWiaMiniDrv：:D rvvalidateitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties) 方法来验证传入值的机会。 WIA 微型驱动程序通过在其自身的驱动程序项树中读取属性，将传入值与任何当前值进行比较。 WIA 服务库提供用于访问这些值的函数。

**IWiaMiniDrv：:D rvvalidateitemproperties** 方法应执行以下任务：

1.  确定项类型。

2.  确定是否应对传入的 WIA 属性执行任何特殊验证。 若要确定正在编写哪些 WIA 属性，WIA 微型驱动程序可以使用 PROPSPEC 结构 (数组，如 Microsoft Windows SDK 文档) 中所述。 建议 WIA 微型驱动程序在处理 PROPSPEC 数组之前确定项类型，以减少每个 IWiaMiniDrv 上的数组遍历数组的需要 **：:D rvvalidateitemproperties** 调用。 如果没有特殊验证要求，或者需要更新设备根项的依赖属性，则只会处理对子项目属性的写入请求。

3.  创建 WIA 属性上下文以访问在 WIA 属性验证期间更改的值，这是更新 WIA 项的依赖属性所必需的。 使用 [**wiasCreatePropContext**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext) 和 **wiasGetChangedValue**_Xxx_ 服务函数。

4.  使用 WIA 服务函数 [**wiasWriteMultiple**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple) 或 **wiasWriteProp**_Xxx_ 更新依赖属性，其中包括更新设置属性后可能已更改的所有有效值。 例如，如果你的 WIA 微型驱动程序支持设置 [**wia \_ IPA \_ DEPTH**](./wia-ipa-depth.md) 属性，则当应用程序更改 [**wia \_ IPA \_ DATATYPE**](./wia-ipa-datatype.md) 属性时，必须更新位深度的有效列表。

    当 [**wia \_ IPA \_ DATATYPE**](./wia-ipa-datatype.md) 属性的值从 wia \_ 数据 \_ 阈值更改为 wia \_ 数据颜色时 \_ ，相关的 WIA \_ IPA \_ depth 属性将从报告一位颜色深度更改为报告24位或48位。

5.  调用 [**wiasValidateItemProperties**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasvalidateitemproperties) 服务函数以允许 WIA 服务验证所有其他属性请求。 这是一个 "全部捕获" 案例;WIA 服务具有内置属性验证。

 

