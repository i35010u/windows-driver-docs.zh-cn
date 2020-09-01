---
title: 驱动程序签名
description: 驱动程序签名
ms.assetid: 1f7d5340-c7be-4b6a-a85e-246dcc78b1fa
keywords:
- 驱动程序签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ed2a07aa22a5db416e4f21263e38ca34e0efa86
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097101"
---
# <a name="driver-signing"></a>驱动程序签名


驱动程序签名将 [数字签名](digital-signatures.md) 与 [驱动程序包](driver-packages.md)相关联。

Windows 设备安装使用 [数字签名](digital-signatures.md) 来验证驱动程序包的完整性，并验证供应商 (软件发行者) 提供驱动程序包的标识。 此外，Windows Vista 和更高版本的 windows Vista 和更高版本的 [内核模式代码签名64策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md) 指定必须对内核模式驱动程序进行签名，以便加载该驱动程序。

**注意**   适用于桌面版的 Windows 10 (Home、Pro、Enterprise 和教育) 和 Windows Server 2016 内核模式驱动程序必须由 Windows 硬件开发人员中心仪表板签名，这需要 EV 证书。 有关详细信息，请参阅 [驱动程序签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)。

Windows 10 (的所有驱动程序都从1507版（硬件开发人员中心) 签署的阈值1）开始，并已 SHA2。  有关特定于操作系统版本的详细信息，请参阅 [按版本签名要求](kernel-mode-code-signing-policy--windows-vista-and-later-.md#signing-requirements-by-version)。

在 windows 10 之前的操作系统上，不会加载内核模式驱动程序二进制文件，使用双重 (SHA1 和 SHA2 从第三方证书供应商处的证书嵌入到 Windows 10 之前的操作系统) 证书，也可能导致 Windows 10 上的系统崩溃。 若要解决此问题，请安装 [KB 3081436](https://support.microsoft.com/help/3081436/cumulative-update-for-windows-10-august-11-2015)。

## <a name="in-this-section"></a>本节内容


-   [Windows 10 S 模式驱动程序要求](Windows10SDriverRequirements.md)
-   [管理签名过程](managing-the-signing-process.md)
-   [在开发和测试期间签署驱动程序](./introduction-to-test-signing.md)
-   [为驱动程序签名以便公开发布](signing-drivers-for-public-release--windows-vista-and-later-.md)
-   [排查已签名驱动程序包的安装和加载问题](./detecting-driver-load-errors.md)
-   [Microsoft 安全公告2880823](/security-updates/SecurityAdvisories/2016/2880823)

有关 Windows Vista 和更高版本的 Windows 上的驱动程序签名的常规信息，请参阅 [在运行 Windows vista 的系统上的面向内核模块的白皮书数字签名](/previous-versions/dotnet/articles/bb530195(v=msdn.10))。


