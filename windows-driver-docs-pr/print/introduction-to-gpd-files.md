---
title: GPD 文件简介
description: GPD 文件简介
keywords:
- 一般打印机说明 WDK Unidrv
- GPD 文件 WDK Unidrv
- Unidrv，GPD 文件
- GPD 文件 WDK Unidrv，关于 GPD 文件
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f3e7836a8937787eae292f3aa32ffe7f29552a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796671"
---
# <a name="introduction-to-gpd-files"></a>GPD 文件简介





GPD 文件用于创建 [Unidrv 微型驱动程序](unidrv-minidrivers.md)。 Unidrv 微型驱动程序包含基于文本的通用打印机说明 (GPD) ，可包含在一个或多个 GPD 文件中。

GPD 文件使用 GPD 语言描述打印机。 文件包含使用 GPD 语言提供以下类型信息的 [GPD 文件项](gpd-file-entries.md) ：

-   描述打印机特征的[打印机属性](printer-attributes.md)。

-   控制打印机操作的[打印机命令](printer-commands.md)。

-   描述可由 Unidrv 控制的打印机功能的[打印机功能](printer-features.md)。

-   [打印机选项](printer-options.md) ，表示可分配给打印机功能的状态。

-   [打印机字体说明](printer-font-descriptions.md) ，用于指定与硬件驻留和字体盒字体相关的特征。

-   描述打印机属性和打印机配置之间的依赖关系的[条件语句](conditional-statements.md)。

GPD 语言还定义了控制以下操作的 GPD 文件项：

[压缩光栅数据](compressing-raster-data.md)

[处理颜色格式](handling-color-formats.md)

[使用 Unidrv 设置半色调](halftoning-with-unidrv.md)

[处理可安装的功能和选项](handling-installable-features-and-options.md)

[描述打印机内存配置](describing-printer-memory-configurations.md)

本介绍部分还介绍了如何[在微型驱动程序中使用多个 GPD 文件](using-multiple-gpd-files-in-a-minidriver.md)，以及如何[使用微型驱动程序中的资源 dll](using-resource-dlls-in-a-minidriver.md)讨论[主单元](master-units.md)。

 

 




