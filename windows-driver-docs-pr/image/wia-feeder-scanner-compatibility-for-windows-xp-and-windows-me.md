---
title: Windows XP 和 Windows Me 的 WIA 送纸器扫描仪兼容性
description: Windows XP 和 Windows Me 的 WIA 送纸器扫描仪兼容性
ms.assetid: 7877943e-ee61-455d-b489-db223e1ddbe1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd54ce7772b237476bbb60450dbfea5f4aad6435
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563020"
---
# <a name="wia-feeder-scanner-compatibility-for-windows-xp-and-windows-me"></a>Windows XP 和 Windows Me 的 WIA 送纸器扫描仪兼容性





本主题介绍与 Windows Vista、 Windows XP 和 Windows me.中的送纸器扫描程序相关的多个兼容性问题

### <a name="changes-from-windows-xp-to-windows-vista"></a>从 Windows XP 到 Windows Vista 的更改

已更改的 Windows XP 和 Windows Vista 之间如何处理扫描的次数。 例如，在 Windows Vista 中，每个功能单元属于单独的类别。 这些类别都包含在[ **WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)属性设置为 WIA\_类别\_的送纸器进纸器和 WIA\_类别\_平板的平板。 如果这两项都是在 Windows Vista 出现在扫描仪上，都必须在项目树中表示。 在 Windows XP 中，在项目树中表示扫描仪功能单元的所有出现的单个扫描项。

下图显示在 Windows XP 中的扫描程序项树。

![说明在 windows xp 中的扫描程序项树的关系图](images/wia-feeder-tree-xp.png)

所有传输关闭此项将会发生，并将用于所有扫描设置 （送纸器以及平板）。

与此相反下, 图显示使用平板和送纸器的扫描仪扫描程序项树在 Windows Vista 中。

![说明使用平板和 windows vista 中的送纸器的扫描仪扫描程序项树的关系图](images/wia-feeder-tree4.png)

此项树表示为独立项树、 平板和送纸器中的项函数单位。 有关此类型的扫描程序的详细信息，请参阅[非双工能力的文档送纸器](non-duplex-capable-document-feeder.md)。

如果您的扫描仪能够支持的双工 （即，扫描的文档的两面），如图所示 Windows Vista 项树。

![说明 windows vista 扫描程序项树与双工的关系图](images/wia-feeder-tree3.png)

上图显示了一个还表示与平板和送纸器的扫描仪的项树。

如图所示而无需在 Windows Vista 中的平板扫描仪项树。

![说明 windows vista 送纸器扫描程序项树的关系图](images/wia-feeder-tree1.png)

在进行双面打印的扫描程序项树和送纸器扫描程序项树中，数据传输始终发生从送纸器项。 扫描设置包含在的送纸器和 （前端和后） 的子项目。

调用其中的前端和后端项目设为相同的设置扫描*基本双工*扫描。 如果前端和后端项目设置相互独立，名为扫描*高级双工*扫描。 有关这些类型的扫描的详细信息，请参阅[简单的双工能力文档送纸器](simple-duplex-capable-document-feeder.md)并[高级 ' 双工能力的文档送纸器](advanced-duplex-capable-document-feeder.md)。

### <a name="compatibility-support-in-windows-vista"></a>在 Windows Vista 的兼容性支持

在 Windows XP Windows Vista 驱动程序和应用程序兼容性是由 Windows Vista 中的 WIA 服务中的兼容性层处理。 此层允许旧应用程序和驱动程序，以用作在 Windows Vista 中相同的方式在 Windows XP 中使用它们。 但是，将会发生一些丢失这些较旧的应用程序和驱动程序与 Windows Vista 应用程序相比和驱动程序中的功能。

### <a name="compatibility-support-in-windows-xp"></a>在 Windows XP 中的兼容性支持

没有为 Windows XP 计算机上使用 Windows Vista 驱动程序的支持极其有限。 如果送纸器扫描程序还支持平板扫描，WIA 平板扫描仪项必须在根项之后扫描程序项树中的第一个 WIA 子项目。 此项树中的关系图进行了说明[非双工能力的文档送纸器](non-duplex-capable-document-feeder.md)主题。 此配置将允许 Windows Vista 驱动程序和 Windows XP 之间的一些兼容性，因为 Windows XP 期望在树中找到的所有扫描设置上的第一项。

有关兼容性层和 Windows XP 和 Windows Me 兼容性的详细信息，请参阅[WIA 平板扫描仪兼容性的 Windows Me 和 Windows XP](wia-flatbed-scanner-compatibility-for-windows-xp-and-windows-me.md)。

 

 




