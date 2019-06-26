---
title: INF 文件概述
description: INF 文件概述
ms.assetid: 94682cba-1f68-416f-af74-99ede81eadc7
keywords:
- INF 文件 WDK 设备安装
- INF 文件 WDK 设备安装创建
- 设备安装程序 WDK 设备安装，INF 文件
- 设备安装 WDK、 INF 文件
- 安装设备 WDK、 INF 文件
- 通过使用 INF 文件安装驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7baa663e05c87ee19208eef04bf788944be02cb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374982"
---
# <a name="overview-of-inf-files"></a>INF 文件概述

Windows 使用安装程序信息 (INF) 文件来安装设备的以下组件：

-   一个或多个驱动程序支持的设备。

-   特定于设备的配置或设置要将设备联机。

INF 文件是包含的所有信息的文本文件，[设备安装组件](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))用于安装驱动程序。 Windows 安装驱动程序使用 INF 文件。 此信息包括：

-   驱动程序名称和位置
-   驱动程序版本信息
-   注册表信息

可以使用*INX*文件以自动创建一个 INF 文件。 INX 文件是包含表示版本信息的字符串变量的 INF 文件。 生成实用工具和[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)工具将替换文本字符串，表示特定硬件体系结构或 framework 版本为 INX 文件中的字符串变量。 有关 INX 文件的详细信息，请参阅[使用 INX 文件转换为创建 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-inx-files-to-create-inf-files)。


请参阅[INF 文件的部分和指令](inf-file-sections-and-directives.md)有关 INF 文件格式的完整说明。
