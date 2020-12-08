---
title: 排查设备和驱动程序安装问题
description: 排查设备和驱动程序安装问题
keywords:
- 设备设置 WDK 设备安装，故障排除
- 设备安装 WDK，故障排除
- 安装设备 WDK，故障排除
- 设备安装的故障排除 WDK
- 设备设置 WDK 设备安装，Setupapi.log
- 安装设备 WDK，Setupapi.log
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7390439deb204a17ebc5d2a7f8a9b43b2483e4c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828589"
---
# <a name="troubleshooting-device-and-driver-installations"></a>排查设备和驱动程序安装问题





你可以使用以下准则来验证设备是否已正确安装或诊断设备安装问题：

-   按照 [使用设备管理器](using-device-manager.md) 查看有关设备的系统信息中所述的步骤进行操作。

-   按照 [Setupapi.log 日志记录 (Windows Vista 和更高版本) ](setupapi-logging--windows-vista-and-later-.md) 或 [setupapi.log 日志记录 (windows Server 2003、Windows XP 和 windows 2000) ](setupapi-logging--windows-server-2003--windows-xp--and-windows-2000-.md) 中介绍的步骤来识别安装错误。

-   在 Windows Vista 和更高版本的 Windows 上，按照 [调试设备安装 (Windows vista 和更高 ](debugging-device-installations--windows-vista-and-later-.md) 版本中所述的步骤) 在设备安装的核心阶段调试 [共同安装程序](writing-a-co-installer.md) 。

-   在 Windows Vista 和更高版本的 Windows 上，按照对 [测试签名驱动程序的安装和加载问题进行疑难解答](./detecting-driver-load-errors.md) 中所述的步骤，诊断与测试签名驱动程序的安装和加载相关的问题。

-   运行测试程序以执行该设备。 这包括随 Windows 驱动程序工具包一起提供的测试和调试工具 (WDK) 。

此外，在 Windows Server 2003、Windows XP 和 Windows 2000 中， [共同安装程序](writing-a-co-installer.md) 可以提供帮助用户诊断设备问题的疑难解答。 有关详细信息，请参阅 [**DIF_TROUBLESHOOTER**](./dif-troubleshooter.md) 。

 

