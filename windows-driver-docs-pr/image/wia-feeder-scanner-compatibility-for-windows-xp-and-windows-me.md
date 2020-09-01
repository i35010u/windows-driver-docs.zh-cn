---
title: Windows XP 和 Windows Me 的 WIA 送纸器扫描仪兼容性
description: Windows XP 和 Windows Me 的 WIA 送纸器扫描仪兼容性
ms.assetid: 7877943e-ee61-455d-b489-db223e1ddbe1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1d63abaffc2802d0cdef1f03abf78440a756d6d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185025"
---
# <a name="wia-feeder-scanner-compatibility-for-windows-xp-and-windows-me"></a>Windows XP 和 Windows Me 的 WIA 送纸器扫描仪兼容性





本主题介绍与 Windows Vista、Windows XP 和 Windows Me 中的进纸器扫描器相关的几个兼容性问题。

### <a name="changes-from-windows-xp-to-windows-vista"></a>从 Windows XP 到 Windows Vista 的更改

在 Windows XP 和 Windows Vista 之间对扫描的处理方式有很多更改。 例如，在 Windows Vista 中，每个功能单元属于单独的类别。 这些类别在 [**wia \_ IPA \_ ITEM \_ CATEGORY**](./wia-ipa-item-category.md) 属性中表示为 \_ \_ 用于进纸器的 wia 类别送纸器和用于平板的 wia \_ 类别 \_ 平板。 如果这两项都存在于 Windows Vista 中的某个扫描器上，则两者都必须在项树中表示。 在 Windows XP 中，项树中有一个表示所有扫描仪功能单元的扫描项。

下图显示了 Windows XP 中的 "扫描仪" 项树。

![说明 windows xp 中的扫描仪项树的关系图](images/wia-feeder-tree-xp.png)

所有传输都将出现在此项目中，并将使用所有扫描设置 (用于进纸器和平板) 。

与此相反，下图显示了在 Windows Vista 中使用平板和送纸器的扫描仪的 "扫描仪" 项树。

![说明在 windows vista 中使用平板和送纸器的扫描仪的扫描程序项目树的关系图](images/wia-feeder-tree4.png)

此项树将函数单元表示为项树中的不同项，即平板和送纸器。 有关此类型的扫描仪的详细信息，请参阅 [支持非双工的文档送纸器](non-duplex-capable-document-feeder.md)。

如果扫描程序可以进行双工 (也就是说，将文档的两侧都扫描) ，Windows Vista 项树将如下图所示。

![说明带双工的 windows vista 扫描仪项树的示意图](images/wia-feeder-tree3.png)

上图显示了一个项树，它还表示同时包含平板和送纸器的扫描仪。

在 Windows Vista 中没有平板的扫描仪的项树如下图所示。

![说明 windows vista 进纸器扫描器项目树的示意图](images/wia-feeder-tree1.png)

在带有双工和进纸器扫描器项目树的 "扫描仪" 项树中，数据传输始终出现在送送纸器项目之外。 扫描设置同时包含在双面和背面) 项 (。

将前和后项设置为相同设置的扫描称为 *基本双工* 扫描。 如果前面和背面的设置彼此独立，则扫描称为 *高级双工* 扫描。 有关这些扫描类型的详细信息，请参阅支持 [双工功能的文档送纸器](simple-duplex-capable-document-feeder.md) 和 [支持高级双面打印的文档送纸器](advanced-duplex-capable-document-feeder.md)。

### <a name="compatibility-support-in-windows-vista"></a>Windows Vista 中的兼容性支持

Windows Vista 中 windows XP 驱动程序和应用程序的兼容性是由 Windows Vista 中的 WIA 服务中的兼容层处理的。 此层允许较旧的应用程序和驱动程序在 Windows Vista 中的使用方式与 Windows XP 中使用的相同。 但是，与 Windows Vista 应用程序和驱动程序相比，这些较旧的应用程序和驱动程序中会出现一些功能损失。

### <a name="compatibility-support-in-windows-xp"></a>Windows XP 中的兼容性支持

Windows XP 计算机上使用 Windows Vista 驱动程序的支持非常有限。 如果您的进纸器扫描仪还支持平板扫描，则 WIA 平板扫描仪项必须是根项后 "扫描程序" 项树中的第一个 WIA 子项。 此项目树由 [不支持双工功能的文档送纸器](non-duplex-capable-document-feeder.md) 主题中的关系图进行说明。 此配置将允许 Windows Vista 驱动程序和 Windows XP 之间的某些兼容性，因为 Windows XP 需要在树中的第一项上找到所有扫描设置。

有关兼容性层和 Windows XP 和 windows Me 兼容性的详细信息，请参阅 [Windows me 和 WINDOWS XP 的 WIA 平板扫描仪兼容性](wia-flatbed-scanner-compatibility-for-windows-xp-and-windows-me.md)。

 

