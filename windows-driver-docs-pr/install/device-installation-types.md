---
title: 设备安装类型
description: Windows 使用 INF 文件在计算机或设备上安装驱动程序包。 所有 Windows 平台都支持通用 INF 文件，而只有适用于桌面版的 Windows 10 (Home、Pro、Enterprise 和教育) 支持旧版 INF 文件。
keywords:
- 设备设置 WDK 设备安装，类型
- 设备安装 WDK，类型
- 安装设备 WDK，类型
- 服务器端安装 WDK 设备安装
- 客户端安装 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e52a6d94549bf7751d685b5e765341bc0156bec6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827719"
---
# <a name="device-installation-types"></a>设备安装类型


Windows 使用 INF 文件在计算机或设备上安装驱动程序包。 所有 Windows 平台都支持通用 INF 文件，而只有适用于桌面版的 Windows 10 (Home、Pro、Enterprise 和教育) 支持旧版 INF 文件。

## <a name="inf-files-for-universal-and-mobile-driver-packages"></a>通用和移动驱动程序包的 INF 文件


如果要构建通用或移动驱动程序包，则必须提供通用 INF 文件。 通用 Inf 仅包含安装和配置设备所需的部分 INF 部分和指令。 无需任何运行时操作，即可在脱机系统上执行这些指令。 有关详细信息，请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

## <a name="inf-files-for-desktop-driver-packages"></a>桌面驱动程序包的 INF 文件


如果要构建仅限桌面的驱动程序包，则 INF 文件可以使用旧版的非通用 INF 语法。

适用于桌面版的 Windows 10 继续支持旧版 INF 行为，如共同安装程序和类安装程序。

 

 





