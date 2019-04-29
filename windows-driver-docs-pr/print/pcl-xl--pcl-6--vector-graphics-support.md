---
title: PCL XL (PCL-6) 矢量图形支持
description: PCL XL (PCL-6) 矢量图形支持
ms.assetid: c8a96506-ed95-44f2-863e-24cbfc919d65
keywords:
- 矢量图形 WDK Unidrv PCL XL
- PCL XL 矢量图形 WDK Unidrv
- 有关 PCL XL 矢量图形的 PCL XL 矢量图形 WDK Unidrv
- PCL-6 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a78a59cc42ce54e3d8bff47c04dfca0cc0a71ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390921"
---
# <a name="pcl-xl-pcl-6-vector-graphics-support"></a>PCL XL (PCL-6) 矢量图形支持





在 Windows XP 及更高版本的 Unidrv 支持 PCL XL 单色图形。 在 Windows Server 2003 及更高版本的 Unidrv 支持 PCL XL 彩色图形。

Unidrv 的支持的 PCL XL (PCL 6) 向量图形使得它可以作为纯光栅格式的替代方法创建 PCL XL 格式的作业数据。 PCL XL 格式通常最适合该设备，并且通常会导致更少的系统开销，更低的输出数据和更快的打印吞吐量。

PCL XL 作业安装程序、 页面设置、 媒体选项和纸张大小使用的大多数当前定义 gpd 分析功能。 但是，实际绘制命令是硬编码 Unidrv 中。 因此，大多数 GPD 文件内的绘图命令将被忽略。 没有必要 GPD 文件中删除这些命令。

本部分包含以下主题：

[写入 PCL XL GPD 文件](writing-a-pcl-xl-gpd-file.md)

[启用对 PCL XL 微型驱动程序中的颜色的支持](enabling-support-for-color-in-pcl-xl-minidrivers.md)

[指定 PCL XL 微型驱动程序中的新设备字体](specifying-new-device-fonts-in-pcl-xl-minidrivers.md)

[使用默认 PCL XL 字体](using-default-pcl-xl-fonts.md)

[安装 PCL XL 微型驱动程序](installing-a-pcl-xl-minidriver.md)

[PCL XL 问题](pcl-xl-issues.md)

 

 




