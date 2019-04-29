---
title: 将 PTP 关联映射到 WIA 文件夹
description: 将 PTP 关联映射到 WIA 文件夹
ms.assetid: 81de26fd-1f93-4018-a628-ad0b0d7468ba
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f6a5f9d49f3f00532de84626825da128ff4033a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380393"
---
# <a name="mapping-ptp-associations-to-wia-folders"></a>将 PTP 关联映射到 WIA 文件夹





对于大多数对象关联，PTP 驱动程序创建 WIA 文件夹项。 WIA\_IPA\_项\_标志属性具有不同的标志集，具体取决于关联类型，此表中所示：

PTP 关联代码关联类型 WIA 项类型标志 （Windows SDK 文档中所述） 0x0000

未定义

WiaItemTypeFolder

0x0001

GenericFolder

WiaItemTypeFolder

0x0002

唱片集

WiaItemTypeFolder

0x0003

TimeSequence

WiaItemTypeFolder | WiaItemTypeBurst

0x0004

HorizontalPanoramic

WiaItemTypeFolder | WiaItemTypeHPanorama

0x0005

VerticalPanoramic

WiaItemTypeFolder | WiaItemTypeVPanorama

0x0006

2DPanoramic

WiaItemTypeFolder

0x0007

AncillaryData

请参阅随附的文本。

 

**SequenceNumber** ObjectInfo 数据集的字段放入 WIA\_IPC\_序列属性。 PTP 驱动程序当前不使用 WIA\_IPC\_XCOORDINATE 和 WIA\_IPC\_YCOORDINATE 属性。 **AssociationDesc**当前未使用 ObjectInfo 数据集的成员。

下图显示了示例 AncillaryData 关联存储在照相机上。 此关联由以及关联的音频和文本的图像组成。

![ptp 树中的辅助数据映像](images/ptp.png)

当 AncillaryData 关联映射到 WIA 文件夹时，非图像对象将成为映像对象的子级，如以下关系图中所示。 图像对象具有在 WIA WiaItemTypeHasAttachments 标志\_IPA\_项\_标志。

![带有附件的 wia 项目](images/wiaattch.png)

 

 




