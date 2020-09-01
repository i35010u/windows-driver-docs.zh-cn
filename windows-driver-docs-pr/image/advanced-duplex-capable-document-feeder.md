---
title: 支持高级双工的文档送纸器
description: 支持高级双工的文档送纸器
ms.assetid: 05b91864-7573-4d99-8a03-701d6cdd650b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55292a0cc5c3cc0225db31412bfba058ff949c95
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188681"
---
# <a name="advanced-duplex-capable-document-feeder"></a>支持高级双工的文档送纸器





高级双工扫描允许应用程序独立配置前页面和上一页设置。

下图说明了支持高级双工和文档送纸器扫描的平板扫描仪的 WIA 项目树。

![说明支持高级双工和文档送纸器扫描的平板扫描仪项树的关系图](images/wia-feeder-tree3.png)

请注意，所扫描页面的正面和背面由项树中的单独子项表示。 这种区别包括 [**wia \_ IPA \_ ITEM \_ category**](./wia-ipa-item-category.md) 属性中的单独类别： wia \_ 类别 \_ 前部和 wia \_ 类别 \_ 。 在执行高级双工扫描的扫描程序中，会单独设置前和后项;它们可能会设置为不同的值。 但是，即使是在能够进行高级双工扫描的扫描仪上，也不能只有前一项或后一项;如果有前一项或后一项，则另一项也必须存在。

该驱动程序指示前面和后面各项都有独立的设置 (也就是说) ，将通过 \_ 在送纸器的 "WIA" " [**WIA \_ \_ \_ \_ **](./wia-dps-document-handling-capabilities.md) " "

### <a name="scanning"></a>扫描

应用程序将导航到 "送纸器" 项以执行文档送纸器扫描。 送纸器项的 WIA 属性应为前端和上一页所共有的受支持的属性值的子集。 应用程序可以选择使用两种类型的数据传输 (标准图像获取或文件夹购置) 影响使用的文档送纸器设置。

### <a name="standard-image-acquisition"></a>标准图像采集

在标准获取或非文件夹获取中，WIA 进纸器项属性设置用于前端和后页， (与) 的简单双工和非双工扫描仪模型相同。

### <a name="folder-image-acquisition"></a>文件夹图像采集

在文件夹获取中，将忽略 WIA 进纸器项的图像设置，而使用前面和背面项的设置。 高级应用程序使用文档送纸器传输的各个可配置设置。 在送纸器扫描器上，即使有子项 (前面和后面的项) ，图像数据也始终从馈送器项获取。

 

