---
title: 版本签名简介
description: 版本签名简介
ms.assetid: 87583d0a-f7c9-49f0-953a-f51891260d75
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2aa5257be05265c900a5047f786ecd9c173817d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519395"
---
# <a name="introduction-to-release-signing"></a>版本签名简介


[驱动程序包](driver-packages.md)应为已发布签名原因如下：

-   若要确保真实性、 完整性和可靠性的驱动程序包。

    Windows 使用数字签名来验证发布服务器的身份并验证该驱动程序发布以来未被修改。

-   若要通过促进自动驱动程序安装可提供最佳用户体验。

    如果未签名驱动程序，[插即用 (PnP) 驱动程序安装策略](digital-signatures-and-pnp-device-installation--windows-vista-and-late.md)要求，系统管理员将手动授权的未签名的驱动程序，安装与安装过程中添加一个额外的步骤。 这个额外的步骤可能可能令人困惑且为一般用户讨厌。

-   若要在 64 位版本的 Windows Vista 和更高版本的 Windows 上运行内核模式驱动程序。

    [内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)适用于 64 位版本的 Windows Vista 及更高版本要求内核模式驱动程序进行签名，以便操作系统加载该驱动程序。

-   若要播放某些返回类型的下一代高级内容，必须对 Windows Vista 和更高版本的 Windows 中的所有内核模式组件进行都签名。 此外，所有用户模式和内核模式组件中受保护的媒体路径 (PMP) 必须都符合 PMP 签名策略。 有关信息 PMP 签名策略，请参阅白皮书[受保护的媒体中的组件 Windows Vista 代码签名](https://go.microsoft.com/fwlink/p/?linkid=69258)。

[硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)已[测试类别](https://go.microsoft.com/fwlink/p/?linkid=189178)多种设备类型。 如果此列表中包含的设备类型的测试类别，应获取驱动程序发行者[WHQL 版本签名](whql-release-signature.md)驱动程序包。

**请注意**  Windows Server 2003 上、 Windows XP 和 Windows 2000 中，从 WHQL 签名的 INF 文件[驱动程序包](driver-packages.md)必须使用[设备安装程序类](device-setup-classes.md)中定义 *%SystemRoot%/inf/Certclas.inf*。 否则，Windows 将视为未签名的驱动程序包。

 

如果驱动程序包是由 WHQL 进行数字签名，才能通过 Windows 更新程序或其他 Microsoft 支持分发机制进行分发。 WHQL 签名 64 位处理器的驱动程序包目录文件，驱动程序发布服务器必须也[嵌入签名](embedded-signatures-in-a-driver-file.md)内核模式驱动程序文件，然后再提交到 WHQL 驱动程序包中。

如果[硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)不具有[测试类别](https://go.microsoft.com/fwlink/p/?linkid=189178)对于你的设备类型，必须使用以下类型的数字签名[发行登录](release-signing-driver-packages.md)在 Windows Vista 和更高版本的 Windows 上的驱动程序包：

-   若要符合内核模式代码签名策略，只需签署驱动程序包[编录文件](catalog-files.md)。 引导启动驱动程序，你必须在内核模式驱动程序文件中嵌入的 SPC 签名并 （可选） 还签署驱动程序包的目录文件。

-   若要符合[PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)的 32 位版本的 Windows Vista 和更高版本的 Windows，可以使用任一一个 SPC 或[商业版本发布证书](commercial-release-certificate.md)进行签名内核模式驱动程序包的目录文件。 这些后一种两个签名类型验证的真实性和完整性的驱动程序，但与 WHQL 版本签名，不会验证该驱动程序的可靠性。

一个 SPC 和商业版本发布证书统称为[发布证书](release-certificates.md)和生成和发布证书的签名被称为*版本签名*。

有关版本签名要求和过程的详细信息，请参阅[版本签名驱动程序包](release-signing-driver-packages.md)。

**请注意**  若要了解版本签名驱动程序包中涉及的步骤，请参阅[如何发布签名驱动程序包](how-to-release-sign-a-driver-package.md)。 本主题提供了摘要版本签名过程中，并指导逐步许多版本签名的示例通过使用*ToastPkg*示例驱动程序包中 Windows Driver Kit (WDK)。

 

 

 





