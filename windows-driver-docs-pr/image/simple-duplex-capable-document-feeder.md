---
title: 支持简单双工的文档送纸器
description: 支持简单双工的文档送纸器
ms.assetid: 0807f02a-5bbf-4ed1-b381-63e1f37a0e2e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: febcb9324b0953de9e8ab3871a46dd9b72016fa5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377330"
---
# <a name="simple-duplex-capable-document-feeder"></a>支持简单双工的文档送纸器





简单的双工扫描前端和后端页使用相同的页设置。 支持进行双面打印的扫描程序应设置双工标志中[ **WIA\_DPS\_文档\_处理\_选择**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)属性。

下图说明了支持简单的双工能力文档送纸器扫描平板扫描仪的 WIA 项树。

![说明支持简单的双工能力文档送纸器扫描平板扫描仪项树的关系图](images/wia-feeder-tree3.png)

请注意项树中的单独的子项目由表示正面和背面正在扫描的页。 此区别包括分隔不同类别中的[ **WIA\_IPA\_项\_类别**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)属性：WIA\_类别\_前端和 WIA\_类别\_返回。 执行基本的双工扫描的扫描仪，请在前端和后端项目将不会设置单独;它们将设置为完全相同的值。

### <a name="scanning"></a>扫描

应用程序导航到要执行文档送纸器扫描的送纸器项。 此项是它们将在此处配置的扫描和每个页面的设置的页面数并设置[ **WIA\_DPS\_文档\_处理\_选择**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)到双面打印设置。 页，对应于信任的文档。 请注意，扫描在四个页面中的两个文档结果。

### <a name="image-acquisition"></a>图像采集

在标准的购买和文件夹获取，WIA 送纸器项目属性设置用于前端和后端页面。 有关标准采集和文件夹获取详细信息，请参阅[高级 ' 双工能力的文档送纸器](advanced-duplex-capable-document-feeder.md)。

 

 




