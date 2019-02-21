---
title: 驱动程序签名
description: 驱动程序签名
ms.assetid: 1f7d5340-c7be-4b6a-a85e-246dcc78b1fa
keywords:
- 驱动程序签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 351e07fd5704f84ad3a85f0bb6cf1d9952c978da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540600"
---
# <a name="driver-signing"></a>驱动程序签名


驱动程序签名相关联[数字签名](digital-signatures.md)与[驱动程序包](driver-packages.md)。

使用 Windows 设备安装[数字签名](digital-signatures.md)验证驱动程序包的完整性并验证供应商 （软件发布者） 的标识由谁提供的驱动程序包。 此外，[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)64 位版本的 Windows Vista 和更高版本的 Windows 指定为要加载的驱动程序必须进行签名的内核模式驱动程序。

**请注意**  Windows 10 桌面版 （主页、 专业版、 企业版和教育版） 和 Windows Server 2016 内核模式驱动程序必须由 Windows 硬件开发人员中心仪表板，这要求 EV 证书进行签名。 有关详细信息，请参阅[Windows 10 中的驱动程序签名更改](http://blogs.msdn.com/b/windows_hardware_certification/archive/2015/04/01/driver-signing-changes-in-windows-10.aspx)。

 

内核模式驱动程序二进制文件嵌入操作系统早于 Windows 10 可能不会加载，或可能会在系统发生崩溃导致 Windows 10 上的第三方证书供应商的双 （SHA1 和 SHA2） 证书签名。 若要解决此问题，请安装[KB 3081436](https://support.microsoft.com/kb/3081436)。

## <a name="in-this-section"></a>本部分内容


-   [数字签名的驱动程序安装的概述](overview-of-digital-signatures-for-driver-installation.md)
-   [Windows 10 S 模式驱动程序要求](Windows10SDriverRequirements.md)
-   [管理签名过程](managing-the-signing-process.md)
-   [在开发和测试签名驱动程序](signing-drivers-during-development-and-test.md)
-   [公开发布的版本的签名的驱动程序](signing-drivers-for-public-release.md)
-   [安装和已签名的驱动程序包的负载问题疑难解答](troubleshooting-install-and-load-problems-with-signed-driver-packages.md)

有关驱动程序的常规信息登录 Windows Vista 和更高版本的 Windows，请参阅白皮书[上的系统运行 Windows Vista 的内核模块数字签名](https://msdn.microsoft.com/library/bb530195)。


 





