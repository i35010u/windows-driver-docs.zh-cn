---
title: WIA 扫描程序项树布局为 Windows Me 和 Windows XP
description: WIA 扫描程序项树布局为 Windows Me 和 Windows XP
ms.assetid: e4824d3a-6439-4ebb-903e-2b592108ddbe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e26a9dc2bf6b51b0b418cca831cfe284244e86cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546909"
---
# <a name="wia-scanner-item-tree-layout-for-windows-xp"></a>Windows XP 的 WIA 扫描程序项树布局


Windows XP WIA 扫描程序项树包含根项目和单个子项目。 下图说明了 WIA 扫描程序项树。

![说明 wia 扫描程序项树的关系图](images/scanner-tree.png)

请参阅[应用程序如何创建 WIA 设备](how-the-application-creates-the-wia-device.md)获取有关如何创建一个项树的示例。 有关其他信息，请参阅[初始化 WIA 微型驱动程序](initializing-the-wia-minidriver.md)，**构建和维护项树**中[WIA 驱动程序服务库](wia-driver-services-library.md)，和[**IWiaMiniDrv::drvInitializeWia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)。 在扫描程序项树的根项目包含所有 WIA 微型驱动程序，以及特定于扫描程序的属性中存在的信息。 特定于扫描程序的属性包括设备制作信息和文档送纸器支持。

子项目表示的设备的数据收集功能，用于将数据传输。 扫描程序的子项应命名以反映它可以执行的操作。

Microsoft 需要将以下名称用于 Windows XP:

**Root**  
表示 WIA 项树中的第一个元素的项。

**平板**  
表示平板扫描仪，无论文档送纸器的项。

**送纸器**  
表示具有仅文档送纸器的扫描仪的项。

对于 Windows Me 和 Windows XP，应用程序必须读取 WIA 属性和第一个子项目上的根项目，以便它能够确定扫描程序设备的功能。

应用程序可以使用 WIA 服务执行以下操作：

-   查询扫描程序功能。

-   设置扫描程序的设备属性。

-   请求数据传输。

应用程序通常预期平板扫描仪，包括那些使用自动文档送纸器 (ADFs)，而无法表示由两个项： 根项目和单个子项目。 从子项目执行所有的数据量。
