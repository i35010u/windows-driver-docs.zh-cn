---
title: 设备安装类型
description: Windows 使用 INF 文件在计算机或设备上安装的驱动程序包。 所有 Windows 平台都支持通用 INF 文件，同时仅 Windows 10 桌面版 （主页、 专业版、 企业版和教育） 支持旧 INF 文件。
ms.assetid: 23b999de-7151-4b4a-b9fc-331909bb8c06
keywords:
- 设备安装程序 WDK 设备安装类型
- 设备安装 WDK，类型
- 安装设备 WDK，类型
- 服务器端的安装 WDK 设备安装
- 客户端安装 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc70de08832eaed9be8af0ff2873add741109ca6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523864"
---
# <a name="device-installation-types"></a>设备安装类型


Windows 使用 INF 文件在计算机或设备上安装的驱动程序包。 所有 Windows 平台都支持通用 INF 文件，同时仅 Windows 10 桌面版 （主页、 专业版、 企业版和教育） 支持旧 INF 文件。

## <a name="inf-files-for-universal-and-mobile-driver-packages"></a>通用和移动驱动程序包的 INF 文件


如果要构建一个通用或移动设备的驱动程序包，则必须提供通用的 INF 文件。 通用 Inf 包含仅 INF 部分和安装和配置设备所需的指令的子集。 可以在脱机的系统中，而无需任何运行时操作执行这些指令。 有关详细信息，请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

## <a name="inf-files-for-desktop-driver-packages"></a>桌面驱动程序包的 INF 文件


如果在构建仅限桌面的驱动程序包，您的 INF 文件可以使用早期的非通用 INF 语法。

面向桌面版本的 Windows 10 继续以支持旧版 INF 行为，例如共同安装程序和类安装程序。

 

 





