---
title: 测试签名的简介
description: 测试签名的简介
ms.assetid: 63d4627d-b92c-489d-accf-16cfb5ac1410
keywords:
- 测试签名驱动程序包 WDK，有关测试签名驱动程序包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2426a79f688a0df2ad5f4794a006b07a7a2c05f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533568"
---
# <a name="introduction-to-test-signing"></a>测试签名的简介


驱动程序应使用测试签名[数字签名](digital-signatures.md)在开发和测试，原因如下：

-   若要简化并自动执行安装。

    如果未签名驱动程序，[插即用 (PnP) 驱动程序安装策略](digital-signatures-and-pnp-device-installation--windows-vista-and-late.md)的 Windows 版本的 Windows Vista 及更高版本需要系统管理员手动授权安装未签名的驱动程序，添加与安装过程的额外步骤。 此额外步骤可能会开发人员和测试人员的工作效率产生负面影响。 此要求不能重写。

-   若要能够加载 64 位版本的 Windows Vista 和更高版本的 Windows 上的内核模式驱动程序。

    默认情况下[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)64 位版本的 Windows Vista 和更高版本的 Windows 需要的内核模式驱动程序进行签名，以便将加载驱动程序。 可以暂时覆盖此要求，以便于开发或调试驱动程序。

-   若要播放某些返回类型的下一代高级内容，必须对 Windows Vista 和更高版本的 Windows 中的所有内核模式组件进行都签名。 此外，所有用户模式和内核模式组件中受保护的媒体路径 (PMP) 必须都符合 PMP 签名策略。 有关信息 PMP 签名策略，请参阅白皮书[受保护的媒体中的组件 Windows Vista 代码签名](https://go.microsoft.com/fwlink/p/?linkid=69258)。

出于这些原因，Windows Vista 和更高版本的 Windows 驱动程序应使用的数字证书创建使用 Microsoft 验证码的测试签名。 此类数字的证书被称为*测试证书*和生成使用测试证书的签名被称为*测试签名*。

**请注意**  Windows Vista 和更高版本的 Windows 支持测试签名的驱动程序仅用于开发和测试目的。 不得用于生产目的或发布给客户测试签名。

 

开发和测试团队可以参与[WHQL 测试签名程序](whql-test-signature-program.md)、 Windows 硬件质量实验室 (WHQL) 将登录 PnP[驱动程序包](driver-packages.md)出于测试目的。 或者，开发和测试团队可以管理他们自己内部的签名过程，并使用以下类型的[测试证书](test-certificates.md)测试签名驱动程序：

-   [MakeCert 测试证书](makecert-test-certificate.md)，其中的数字证书创建[ **MakeCert** ](https://msdn.microsoft.com/library/windows/hardware/ff548309)工具。

-   [商业测试证书](commercial-test-certificate.md)，这是由 Microsoft 根证书程序成员的 CA 颁发的数字证书。

-   [企业 CA 测试证书](enterprise-ca-test-certificate.md)，这是部署的企业 CA 的数字证书。

有关如何测试团队对进行签名的驱动程序包后，团队创建、 获取，或提供一个测试证书的信息，请参阅[测试签名驱动程序包](test-signing-driver-packages.md)。

有关如何安装测试签名的驱动程序包的信息，请参阅[Installing Test-Signed 驱动程序包](installing-test-signed-driver-packages.md)。

为了便于早期驱动程序开发和调试，可以暂时禁用内核模式代码签名需要加载和测试未签名的内核模式驱动程序。 但是，不能禁用需要系统管理员进行授权的未签名的驱动程序安装的即插即用驱动程序安装策略。 有关如何安装未签名的驱动程序的详细信息，请参阅[开发和测试期间安装未签名的驱动程序](installing-an-unsigned-driver-during-development-and-test.md)。

有关最适当的工具来使用测试签名驱动程序的包的信息，请参阅[签名的驱动程序的工具](https://msdn.microsoft.com/library/windows/hardware/ff552958)。

**请注意**  若要获取更好地了解测试签名驱动程序包中涉及的步骤，请参阅[如何测试签名驱动程序包](how-to-test-sign-a-driver-package.md)。 本主题提供了摘要测试签名过程中，并通过的测试签名的许多示例使用的步骤*ToastPkg*示例[驱动程序包](driver-packages.md)Windows Driver Kit (WDK) 中。

 

 

 





