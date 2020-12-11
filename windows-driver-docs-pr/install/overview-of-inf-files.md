---
title: INF 文件概述
description: INF 文件概述
keywords:
- INF 文件 WDK 设备安装
- INF 文件 WDK 设备安装，创建
- 设备设置 WDK 设备安装，INF 文件
- 设备安装 WDK，INF 文件
- 安装设备 WDK，INF 文件
- 使用 INF 文件安装驱动程序
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: ba741650f7985c7b5488a943a91a46ad94038907
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832671"
---
# <a name="overview-of-inf-files"></a>INF 文件概述

Windows 使用安装信息 (INF) 文件安装设备的下列组件：

-   支持设备的一个或多个驱动程序。

-   使设备联机的设备特定的配置或设置。

INF 文件是一个文本文件，其中包含[设备安装组件](/previous-versions/ff541277(v=vs.85))安装驱动程序时使用的所有信息。 Windows 使用 INF 文件安装驱动程序。 此信息包括：

-   驱动程序名称和位置
-   驱动程序版本信息
-   注册表信息

可以使用 INX  文件来自动创建 INF 文件。 INX 文件是一个 INF 文件，其中包含表示版本信息的字符串变量。 生成实用工具和 [Stampinf](../devtest/stampinf.md) 工具将 INX 文件中的字符串变量替换为表示特定硬件体系结构或框架版本的文本字符串。 有关 INX 文件的详细信息，请参阅[使用 INX 文件创建 INF 文件](../wdf/using-inx-files-to-create-inf-files.md)。


有关 INF 文件格式的完整说明，请参阅 [INF 文件部分](inf-classinstall32-section.md)和 [INF 文件指令](inf-addcomponent-directive.md)。
