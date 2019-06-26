---
title: 排查设备和驱动程序安装问题
description: 排查设备和驱动程序安装问题
ms.assetid: 1ffad62b-140d-4a0a-9174-245e0344e605
keywords:
- 设备安装程序 WDK 设备安装，故障排除
- 设备安装 WDK，故障排除
- 安装设备 WDK，故障排除
- 设备安装 WDK 疑难解答
- 设备安装程序 WDK 设备安装，安装程序 Api
- 安装设备 WDK，安装程序 Api
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff801448db37d9ddb27ed0dbc7b6d38f7a684254
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371279"
---
# <a name="troubleshooting-device-and-driver-installations"></a>排查设备和驱动程序安装问题





可以使用以下准则来验证你的设备正确安装或诊断你的设备安装的问题：

-   按照中所述的步骤[使用设备管理器](using-device-manager.md)若要查看有关设备的系统信息。

-   按照中所述的步骤[SetupAPI 日志记录 （Windows Vista 和更高版本）](setupapi-logging--windows-vista-and-later-.md)或[SetupAPI 日志记录 （Windows Server 2003、 Windows XP 和 Windows 2000）](setupapi-logging--windows-server-2003--windows-xp--and-windows-2000-.md)来标识安装错误。

-   在 Windows Vista 和更高版本的 Windows，请按照中所述的步骤[调试设备安装 （Windows Vista 和更高版本）](debugging-device-installations--windows-vista-and-later-.md)调试[共同安装程序](writing-a-co-installer.md)设备的核心阶段期间安装。

-   在 Windows Vista 和更高版本的 Windows，请按照中所述的步骤[故障排除安装和测试签名的驱动程序的负载问题](troubleshooting-install-and-load-problems-with-signed-driver-packages.md)诊断相关的问题： 安装和加载的测试签名驱动程序。

-   运行测试程序，以实现设备。 这包括提供与 Windows Driver Kit (WDK) 的测试和调试工具。

此外，在 Windows Server 2003、 Windows XP 和 Windows 2000[共同安装程序](writing-a-co-installer.md)可以提供故障排除的工具，可帮助诊断问题与你的设备的用户。 请参阅[ **DIF_TROUBLESHOOTER** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-troubleshooter)有关详细信息。

 

 





