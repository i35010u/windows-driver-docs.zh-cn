---
title: 驱动程序签名
description: 驱动程序签名
ms.assetid: 1f7d5340-c7be-4b6a-a85e-246dcc78b1fa
keywords:
- 驱动程序签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 839cac6ab06b61c20054efa133a65b4e9126e8a5
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557728"
---
# <a name="driver-signing"></a>驱动程序签名


驱动程序签名将[数字签名](digital-signatures.md)与[驱动程序包](driver-packages.md)相关联。

Windows 设备安装使用[数字签名](digital-signatures.md)来验证驱动程序包的完整性并验证提供驱动程序包的供应商（软件发行者）的标识。 此外，Windows Vista 和更高版本的 windows Vista 和更高版本的[内核模式代码签名64策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)指定必须对内核模式驱动程序进行签名，以便加载该驱动程序。

**注意**   适用于桌面版的 windows 10 （家庭版、专业版、企业版和教育版）和 Windows Server 2016 内核模式驱动程序必须由 Windows 硬件开发人员中心仪表板签名，这需要 EV 证书。 有关详细信息，请参阅[驱动程序签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)。

所有适用于 Windows 10 的驱动程序（从版本1507开始，阈值为1）由硬件开发人员中心签名，SHA2 签名。  有关特定于操作系统版本的详细信息，请参阅[按版本签名要求](kernel-mode-code-signing-policy--windows-vista-and-later-.md#signing-requirements-by-version)。

在 windows 10 之前的操作系统上，从第三方证书供应商处使用双重（SHA1 和 SHA2）证书嵌入的内核模式驱动程序二进制文件可能不会加载，也可能导致 Windows 10 上的系统崩溃。 若要解决此问题，请安装[KB 3081436](https://support.microsoft.com/help/3081436/cumulative-update-for-windows-10-august-11-2015)。

## <a name="in-this-section"></a>在本节中


-   [适用于驱动程序安装的数字签名概述](overview-of-digital-signatures-for-driver-installation.md)
-   [Windows 10 S 模式驱动程序要求](Windows10SDriverRequirements.md)
-   [管理签名过程](managing-the-signing-process.md)
-   [在开发和测试期间签署驱动程序](signing-drivers-during-development-and-test.md)
-   [为驱动程序签名以便公开发布](signing-drivers-for-public-release--windows-vista-and-later-.md)
-   [排查已签名驱动程序包的安装和加载问题](troubleshooting-install-and-load-problems-with-signed-driver-packages.md)
-   [Microsoft 安全公告2880823](https://docs.microsoft.com/security-updates/SecurityAdvisories/2016/2880823)

有关 Windows Vista 和更高版本的 Windows 上的驱动程序签名的常规信息，请参阅[在运行 Windows vista 的系统上的面向内核模块的白皮书数字签名](https://docs.microsoft.com/previous-versions/dotnet/articles/bb530195(v=msdn.10))。


 





