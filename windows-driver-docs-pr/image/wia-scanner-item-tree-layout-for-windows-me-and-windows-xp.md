---
title: Windows Me 和 Windows XP 的 WIA 扫描仪项树布局
description: Windows Me 和 Windows XP 的 WIA 扫描仪项树布局
ms.assetid: e4824d3a-6439-4ebb-903e-2b592108ddbe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 136872c780f3c9e4d54a04925f4ba96cab1b4736
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188881"
---
# <a name="wia-scanner-item-tree-layout-for-windows-xp"></a>适用于 Windows XP 的 WIA 扫描器项树布局


Windows XP 的 WIA 扫描器项树包含一个根项和一个子项。 下图说明了 WIA 扫描器项树。

![说明 wia 扫描器项树的关系图](images/scanner-tree.png)

有关如何创建项树的示例，请参阅 [应用程序如何创建 WIA 设备](how-the-application-creates-the-wia-device.md) 。 有关其他信息，请参阅 [初始化 Wia 微型驱动程序](initializing-the-wia-minidriver.md)、 **生成和维护** [WIA 驱动程序服务库](wia-driver-services-library.md)中的项树和 [**IWiaMiniDrv：:d rvinitializewia**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)。 扫描仪项树中的根项包含所有 WIA 微型驱动程序中存在的信息，以及特定于扫描程序的属性。 扫描仪特定的属性包括设备光学信息和文档送纸器支持。

子项表示设备的数据收集功能，用于传输数据。 应将扫描仪的子项命名为，以反映它可以执行的操作。

Microsoft 需要为 Windows XP 提供以下名称：

**Root**  
表示 WIA 项树中第一个元素的项。

**平板**  
表示平板扫描仪的项，有或不带文档送纸器。

**放**  
表示仅具有文档送纸器的扫描仪的项。

对于 Windows Me 和 Windows XP，应用程序必须读取根项和第一个子项目上的 WIA 属性，以便它可以确定扫描仪设备的功能。

应用程序可以使用 WIA 服务来执行以下操作：

-   查询扫描程序功能。

-   设置扫描程序设备属性。

-   请求数据传输。

应用程序通常需要平板扫描仪，其中包括具有自动文档送纸送 (ADFs) 的扫描程序，这些扫描程序由两个项表示：根项和单个子项。 所有数据传输都是从子项目中执行的。