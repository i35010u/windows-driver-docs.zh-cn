---
title: PCL XL (PCL-6) 矢量图形支持
description: PCL XL (PCL-6) 矢量图形支持
keywords:
- 矢量图形 WDK Unidrv，PCL XL
- PCL XL 向量图形 WDK Unidrv
- PCL XL 矢量图形 WDK Unidrv，关于 PCL XL 矢量图形
- PCL-6 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90ede5ad567638aaa2ec54004cafdab905967e65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807617"
---
# <a name="pcl-xl-pcl-6-vector-graphics-support"></a>PCL XL (PCL-6) 矢量图形支持





Windows XP 和更高版本中的 Unidrv 支持 PCL XL 单色图形。 Windows Server 2003 和更高版本中的 Unidrv 支持 PCL XL 彩色图形。

Unidrv 支持 PCL XL (PCL-6) 矢量图形允许它以 PCL XL 格式创建作业数据，作为纯光栅格式的替代方法。 PCL XL 格式通常是设备的最佳格式，通常导致系统开销较少、输出数据较少，打印吞吐量更快。

PCL XL 使用大多数当前定义的 GPD 功能进行作业设置、页面设置、媒体选择和纸张大小。 但是，实际的绘图命令在 Unidrv 中是硬编码的。 因此，GPD 文件中的大多数绘图命令都将被忽略。 无需从 GPD 文件中删除这些命令。

本节包含下列主题：

[编写 PCL XL GPD 文件](writing-a-pcl-xl-gpd-file.md)

[启用对 PCL XL 微型驱动程序中的颜色的支持](enabling-support-for-color-in-pcl-xl-minidrivers.md)

[在 PCL XL 微型驱动程序中指定新的设备字体](specifying-new-device-fonts-in-pcl-xl-minidrivers.md)

[使用默认的 PCL XL 字体](using-default-pcl-xl-fonts.md)

[安装 PCL XL 微型驱动程序](installing-a-pcl-xl-minidriver.md)

[PCL XL 问题](pcl-xl-issues.md)

 

 




