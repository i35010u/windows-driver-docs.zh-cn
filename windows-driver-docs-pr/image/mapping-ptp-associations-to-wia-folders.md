---
title: 将 PTP 关联映射到 WIA 文件夹
description: 将 PTP 关联映射到 WIA 文件夹
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0afb176a2f0f78b5c418de6b30a27dd3491996f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820749"
---
# <a name="mapping-ptp-associations-to-wia-folders"></a>将 PTP 关联映射到 WIA 文件夹





对于大多数对象关联，PTP 驱动程序会创建一个 WIA 文件夹项。 WIA \_ IPA \_ ITEM \_ FLAGS 属性的标志集不同，具体取决于关联类型，如下表所示：

Windows SDK 文档中所述的 PTP 关联代码关联类型 WIA 项类型标志 () 0x0000

Undefined

WiaItemTypeFolder

0x0001

GenericFolder

WiaItemTypeFolder

0x0002

相册：

WiaItemTypeFolder

0x0003

TimeSequence

WiaItemTypeFolder |WiaItemTypeBurst

0x0004

HorizontalPanoramic

WiaItemTypeFolder |WiaItemTypeHPanorama

0x0005

VerticalPanoramic

WiaItemTypeFolder |WiaItemTypeVPanorama

0x0006

2DPanoramic

WiaItemTypeFolder

0x0007

AncillaryData

请参阅附带文本。

 

ObjectInfo 数据集的 **SequenceNumber** 字段放入 WIA \_ IPC \_ SEQUENCE 属性中。 PTP 驱动程序当前不使用 WIA \_ ipc \_ XCOORDINATE 和 wia \_ ipc \_ YCOORDINATE 属性。 当前未使用 ObjectInfo 数据集的 **AssociationDesc** 成员。

下图显示了存储在照相机上的示例 AncillaryData 关联。 此关联包括图像以及关联的音频和文本。

![含辅助数据的映像的 ptp 树](images/ptp.png)

当 AncillaryData 关联映射到 WIA 文件夹时，nonimage 对象将成为 image 对象的子项，如下图所示。 Image 对象在 WIA \_ IPA ITEM 标志中设置了 WiaItemTypeHasAttachments \_ 标志 \_ 。

![带有附件的 wia 项](images/wiaattch.png)

 

 




