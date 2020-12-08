---
title: 内核模式代码签名要求
description: 内核模式代码签名要求
keywords:
- 驱动程序签名 WDK，内核模式代码签名要求
- 对驱动程序进行签名 WDK，内核模式代码签名要求
- 数字签名 WDK，内核模式代码签名要求
- 签名 WDK，内核模式代码签名要求
- 内核模式代码签名要求 WDK
- 内核模式驱动程序签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea350818ce717313eb5e27c8b634a431133b2bbf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831397"
---
# <a name="kernel-mode-code-signing-requirements"></a>内核模式代码签名要求


从 Windows Vista 开始，内核模式代码签名策略控制是否将加载内核模式驱动程序。 签名要求取决于 Windows 操作系统的版本，以及在开发和测试驱动程序的过程中是否对驱动程序进行公共发布或开发团队签名。 还有与 PnP 设备和驱动程序安装有关的 [签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md) 。

虚拟驱动程序与实际硬件驱动程序具有相同的要求。 换句话说，它们必须符合针对的操作系统版本的要求。

有关签名和仪表板提交的信息，请参阅 [获取 Microsoft 为多个 Windows 版本签名的驱动程序](../dashboard/get-drivers-signed-by-microsoft-for-multiple-windows-versions.md)。

### <a name="kernel-mode-code-signing-requirements-for-public-release-of-a-driver"></a><a href="" id="kernel-mode-code-signing-requirements-for-public-release-of-a-driver"></a> Kernel-Mode 公开发布驱动程序的代码签名要求

> [!NOTE]
> 从 Windows 10 版本1607开始，Windows 将不会加载任何新的内核模式驱动程序，这些驱动程序未由 Microsoft 通过 [硬件开发人员中心](../dashboard/register-for-the-hardware-program.md)进行签名。  有效的签名可通过 [硬件认证](../dashboard/hardware-certification-submissions.md) 或 [证明](../dashboard/attestation-signing-a-kernel-driver-for-public-release.md)获得。 


<a href="" id="--------64-bit-versions-of-windows-starting-with-"></a>**64 位版本的 windows （从 Windows Vista 开始）**  
内核模式代码签名策略要求对内核模式驱动程序进行签名，如下所示：

-   内核模式启动驱动程序必须将嵌入式 [软件发行者证书 (SPC) ](software-publisher-certificate.md) 签名。 这适用于任何类型的 PnP 或非 PnP 内核模式启动驱动程序。

-   非 PnP 内核模式驱动程序不是启动启动驱动程序必须具有具有 SPC 签名的 [目录文件](catalog-files.md) ，或者驱动程序文件必须包含嵌入的 SPC 签名。

-   不是启动启动驱动程序的 PnP 内核模式驱动程序必须具有嵌入的 SPC 签名、具有 [WHQL 版本签名](whql-release-signature.md)的目录文件或具有 SPC 签名的目录文件。 尽管内核模式代码签名策略不要求对 PnP 驱动程序的编录文件进行签名，但 PnP 设备安装仅当驱动程序的编录文件也已签名时才将驱动程序视为已签名。

<a href="" id="32-bit-versions-of-windows"></a>**32位版本的 Windows**  
Windows Vista 和更高版本的 Windows 仅对以下驱动程序强制实施内核模式驱动程序签名策略：

-   流式传输受保护媒体的驱动程序。 有关这些要求的详细信息，请参阅 [Windows Vista 和更高版本 (受保护媒体组件的代码签名) ](/windows-hardware/test/hlk/)

-   内核模式 *启动-启动驱动程序*。

### <a name="kernel-mode-code-signing-requirements-during-development-and-test"></a><a href="" id="kernel-mode-code-signing-requirements-during-development-and-test"></a> 在开发和测试期间 Kernel-Mode 代码签名要求

<a href="" id="--------64-bit-versions-of-windows-starting-with-"></a>**64 位版本的 windows （从 Windows Vista 开始）**  
内核模式代码签名策略要求对内核模式驱动程序进行 [测试签名](test-signing-driver-packages.md) ，并 [启用](the-testsigning-boot-configuration-option.md)测试签名。 测试签名可以是 [WHQL 测试签名](whql-test-signature-program.md) ，也可以由 [测试证书](./makecert-test-certificate.md)内部生成。 驱动程序必须对其进行测试签名，如下所示：

-   内核模式 *启动启动驱动程序* 必须具有嵌入的测试签名。 这适用于任何类型的 PnP 或非 PnP 内核模式驱动程序。

-   不是 *启动启动驱动程序* 的内核模式驱动程序必须包含测试签名的 [目录文件](catalog-files.md) 或驱动程序文件必须包含嵌入的测试签名。 这适用于任何类型的 PnP 或非 PnP 内核模式驱动程序。

<a href="" id="32-bit-versions-of-windows"></a>**32位版本的 Windows**  
Windows Vista 和更高版本的 Windows 仅对以下驱动程序强制实施内核模式驱动程序签名策略：

-   流式传输受保护媒体的驱动程序。 有关这些要求的详细信息，请参阅 [Windows Vista 和更高版本 (受保护媒体组件的代码签名) ](/windows-hardware/test/hlk/)

-   内核模式 *启动-启动驱动程序*。

