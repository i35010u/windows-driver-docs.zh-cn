---
title: GPD 文件简介
description: GPD 文件简介
ms.assetid: f29415cf-d8ca-42a2-bbae-2be53e3621a6
keywords:
- 通用打印机说明 WDK Unidrv
- GPD 文件 WDK Unidrv
- Unidrv，GPD 文件
- GPD 文件 WDK Unidrv 有关 GPD 文件
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7a0bc4fab91134ad6181dcec2bfca1c9d93a02d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377219"
---
# <a name="introduction-to-gpd-files"></a>GPD 文件简介





GPD 文件将用于创建[Unidrv 微型驱动程序](unidrv-minidrivers.md)。 Unidrv 微型驱动程序包含，可以在一个或多个 GPD 文件中包含基于文本的泛型打印机说明 (GPD)。

GPD 文件使用 GPD 语言来描述打印机。 这些文件包含[GPD 文件条目](gpd-file-entries.md)，使用 GPD 语言提供以下类型的信息：

-   [打印机属性](printer-attributes.md)，用于描述打印机的特征。

-   [打印机命令](printer-commands.md)控制的打印机操作。

-   [打印机功能](printer-features.md)描述可以由 Unidrv 控制的打印机功能。

-   [打印机选项](printer-options.md)表示可分配给打印机功能的状态。

-   [打印机字体说明](printer-font-descriptions.md)，用于指定与硬件驻留和插件字体相关联的特性。

-   [条件语句](conditional-statements.md)，用于描述打印机属性和打印机的配置之间的依赖关系。

GPD 语言还定义 GPD 文件项的控制以下操作：

[光栅数据进行压缩](compressing-raster-data.md)

[处理颜色格式](handling-color-formats.md)

[使用 Unidrv 半色调](halftoning-with-unidrv.md)

[处理可安装的功能和选项](handling-installable-features-and-options.md)

[描述打印机内存配置](describing-printer-memory-configurations.md)

本介绍性部分还包括程序开发的讨论[掌握单位](master-units.md)，[微型驱动程序中使用多个 GPD 文件](using-multiple-gpd-files-in-a-minidriver.md)，并[使用微型驱动程序中的资源 Dll](using-resource-dlls-in-a-minidriver.md)。

 

 




