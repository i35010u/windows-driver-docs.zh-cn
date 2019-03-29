---
title: 内核模式代码签名要求
description: 内核模式代码签名要求
ms.assetid: da02fcb3-d073-42cd-8247-71e2e9e93f65
keywords:
- 驱动程序签名 WDK，内核模式代码签名要求
- 签署驱动程序 WDK，内核模式代码签名要求
- 数字签名 WDK，内核模式代码签名要求
- 签名 WDK，内核模式代码签名要求
- 内核模式代码签名要求 WDK
- 内核模式驱动程序签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 442d37abc86ca0b8936032b859602b9da69175e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566139"
---
# <a name="kernel-mode-code-signing-requirements"></a>内核模式代码签名要求


从 Windows Vista，内核模式代码签名的策略控制是否将加载的内核模式驱动程序开始。 签名要求取决于 Windows 操作系统的版本以及是否驱动程序是正被签名的公开发布的版本或由开发团队在开发和测试驱动程序的过程。 此外，还有[签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)，适用于安装的即插即用设备和驱动程序。

虚拟驱动程序必须与实际的硬件驱动程序相同的要求。 换而言之，它们必须符合对于它们的目标为其操作系统版本要求。

有关签名和仪表板提交的信息，请参阅[获取多个 Windows 版本的 Microsoft 签名的驱动程序](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-drivers-signed-by-microsoft-for-multiple-windows-versions)。

### <a href="" id="kernel-mode-code-signing-requirements-for-public-release-of-a-driver"></a> 内核模式代码签名的驱动程序的公开发布版本要求

> [!NOTE]
> 从 Windows 10，版本 1607，Windows 将不会加载任何新的内核模式驱动程序不由 Microsoft 通过签名这[硬件开发人员中心](https://docs.microsoft.com/windows-hardware/drivers/dashboard/register-for-the-hardware-program)。  可以通过以下任一方法获取有效的签名[硬件认证](https://docs.microsoft.com/windows-hardware/drivers/dashboard/hardware-certification-submissions)或[证明](https://docs.microsoft.com/windows-hardware/drivers/dashboard/attestation-signing-a-kernel-driver-for-public-release)。 


<a href="" id="--------64-bit-versions-of-windows-starting-with-"></a> **64 位版本的 Windows 与 Windows Vista 一起启动**  
内核模式代码签名策略要求内核模式驱动程序进行签名，如下所示：

-   内核模式引导启动驱动程序必须具有嵌入[软件发布者证书 (SPC)](software-publisher-certificate.md)签名。 这适用于任何类型的即插即用或为非 PnP 内核模式下启动开始驱动程序。

-   不是一个引导启动驱动程序的非 PnP 内核模式驱动程序必须拥有[编录文件](catalog-files.md)一个 SPC 签名或驱动程序文件必须包含嵌入的 SPC 签名。

-   不是一个引导启动驱动程序的即插即用的内核模式驱动程序必须具有任一的嵌入式的 SPC 签名的编录文件[WHQL 版本签名](whql-release-signature.md)，或使用 SPC 签名目录文件。 虽然内核模式代码签名策略不需要即插即用驱动程序的目录文件进行签名，即插即用设备安装会将驱动程序，因为签名才还签名的驱动程序的目录文件。

<a href="" id="32-bit-versions-of-windows"></a>**32 位版本的 Windows**  
Windows Vista 和更高版本的 Windows 强制实施仅对以下驱动程序的内核模式驱动程序签名策略：

-   流式传输受保护的媒体的驱动程序。 有关这些要求的详细信息，请参阅[代码签名的受保护的媒体组件 （Windows Vista 和更高版本）](https://go.microsoft.com/fwlink/p/?linkid=69258)

-   内核模式*引导启动驱动程序*。

### <a href="" id="kernel-mode-code-signing-requirements-during-development-and-test"></a> 内核模式代码签名要求在开发和测试过程

<a href="" id="--------64-bit-versions-of-windows-starting-with-"></a> **64 位版本的 Windows 与 Windows Vista 一起启动**  
内核模式代码签名策略要求内核模式驱动程序[测试签名](test-signing-driver-packages.md)并且该测试签名[启用](the-testsigning-boot-configuration-option.md)。 测试签名可以采取[WHQL 测试签名](whql-test-signature-program.md)或者由内部生成[测试证书](test-certificates.md)。 驱动程序必须进行测试签名，如下所示：

-   内核模式*引导启动驱动程序*必须具有嵌入的测试签名。 这适用于任何类型的即插即用或为非 PnP 内核模式驱动程序。

-   不是内核模式驱动程序*引导启动驱动程序*必须具有任一测试签名[编录文件](catalog-files.md)或驱动程序文件必须包含嵌入式的测试签名。 这适用于任何类型的即插即用或为非 PnP 内核模式驱动程序。

<a href="" id="32-bit-versions-of-windows"></a>**32 位版本的 Windows**  
Windows Vista 和更高版本的 Windows 强制实施仅对以下驱动程序的内核模式驱动程序签名策略：

-   流式传输受保护的媒体的驱动程序。 有关这些要求的详细信息，请参阅[代码签名的受保护的媒体组件 （Windows Vista 和更高版本）](https://go.microsoft.com/fwlink/p/?linkid=69258)

-   内核模式*引导启动驱动程序*。

 

 





