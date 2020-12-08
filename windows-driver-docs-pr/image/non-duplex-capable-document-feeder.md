---
title: 支持非双工的文档送纸器
description: 支持非双工的文档送纸器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a6453067beb05ac4ba080fda6b95aa26255bb03
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829695"
---
# <a name="non-duplex-capable-document-feeder"></a>支持非双工的文档送纸器





下图显示了平板扫描仪的 WIA 项树，该树支持简单的 (非双工) 文档送纸器扫描。

![说明支持非双工文档送纸器扫描的平板扫描仪的 wia 项目树的关系图](images/wia-feeder-tree4.png)

带有送纸器 (或自动文档送纸器的扫描仪) 无需具有平台。 下图演示了没有平板或双面打印器的进纸器扫描仪的项目树。

![说明没有平板或双面打印器的进纸器扫描仪的项目树的关系图](images/wia-feeder-tree2.png)

只有当扫描仪上没有平板时，才能省略平板物品。 同样，具有送纸器的任何扫描仪的 "项目树" 中必须存在 "送纸器" 项。 "进纸器" 项用于控制设置，如基本扫描 (无双工或单面) ，简单双工 (相同的前和后项) ，以及高级双工扫描 (独立的前端和后项) 。

### <a name="scanning"></a>扫描

应用程序将导航到 "送纸器" 项以执行文档送纸器扫描。 在此项目中，应用程序将配置要扫描的页数以及每个页面的设置。 请注意，扫描三个文档会生成三个页面。

### <a name="image-acquisition"></a>图像采集

在标准获取和文件夹获取中，WIA 进纸器项目属性设置用于所有正面页面。 有关标准获取和获取文件夹的详细信息，请参阅 [高级 Duplex-Capable 文档送纸器](advanced-duplex-capable-document-feeder.md)。

 

 




