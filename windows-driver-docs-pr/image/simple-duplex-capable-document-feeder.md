---
title: 支持简单双工的文档送纸器
description: 支持简单双工的文档送纸器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ab8ce030de605b73274f9c386d27e82edd66304
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802459"
---
# <a name="simple-duplex-capable-document-feeder"></a>支持简单双工的文档送纸器





简单的双工扫描使用相同页面设置来用于前后页面。 支持双工的扫描仪应在 [**WIA \_ DPS \_ 文档 \_ 处理 \_ 选择**](./wia-dps-document-handling-select.md) 属性中设置双工标志。

下图说明了平板扫描仪的 WIA 项目树，它支持支持支持双工的文档送纸器扫描。

![说明支持简单双面支持的文档送纸器扫描的平板扫描仪项树的关系图](images/wia-feeder-tree3.png)

请注意，所扫描页面的正面和背面由项树中的单独子项表示。 这种区别包括 [**wia \_ IPA \_ ITEM \_ category**](./wia-ipa-item-category.md) 属性中的单独类别： wia \_ 类别 \_ 前部和 wia \_ 类别 \_ 。 在执行基本双工扫描的扫描程序中，不会单独设置前面和背面项;它们将被设置为完全相同的值。

### <a name="scanning"></a>扫描

应用程序将导航到 "送纸器" 项以执行文档送纸器扫描。 在此项中，他们将配置要扫描的页数以及每个页面的设置，并设置 [**WIA \_ DPS \_ 文档 \_ 处理 \_ 选择**](./wia-dps-document-handling-select.md) "双面" 设置。 页面对应于文档的一侧。 请注意，扫描两个文档会导致四页。

### <a name="image-acquisition"></a>图像采集

在标准获取和文件夹获取中，WIA 进纸器项属性设置用于前后页面。 有关标准获取和获取文件夹的详细信息，请参阅 [高级 Duplex-Capable 文档送纸器](advanced-duplex-capable-document-feeder.md)。

 

