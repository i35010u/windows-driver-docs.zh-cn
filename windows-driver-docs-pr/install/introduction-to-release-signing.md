---
title: 发布签名简介
description: 发布签名简介
ms.assetid: 87583d0a-f7c9-49f0-953a-f51891260d75
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59c6921ed89c4262cef184b481d6bcc5b6de39c9
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733262"
---
# <a name="introduction-to-release-signing"></a>发布签名简介


由于以下原因，[驱动程序包](driver-packages.md)应为 release 签名：

-   确保驱动程序包的可靠性、完整性和可靠性。

    Windows 使用数字签名来验证发行者的身份，并验证自发布后该驱动程序是否已更改。

-   通过促进自动驱动程序安装来提供最佳用户体验。

    如果驱动程序未签名，则 [即插即用 (PnP) 驱动程序安装策略](digital-signatures-and-pnp-device-installation--windows-vista-and-late.md) 要求系统管理员手动授权安装未签名的驱动程序，并在安装过程中添加额外的步骤。 这一额外步骤可能会令用户感到困惑，并难点用户。

-   在 Windows Vista 和更高版本的 Windows 的64位版本上运行内核模式驱动程序。

    64位版本的 Windows Vista 和更高版本的 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md) 要求对内核模式驱动程序进行签名，以便操作系统加载驱动程序。

-   若要播放特定类型的下一代高级内容，Windows Vista 和更高版本的 Windows 中的所有内核模式组件都必须进行签名。 此外，受保护媒体路径 (PMP) 中的所有用户模式和内核模式组件必须符合 PMP 签名策略。 有关 PMP 签名策略的信息，请参阅 [Windows Vista 中的针对受保护媒体组件的白皮书代码签名](/windows-hardware/test/hlk/)。

[硬件认证工具包 (HCK) ](/previous-versions/windows/hardware/hck/jj124227(v=vs.85))包含各种设备类型的[测试类别](/windows-hardware/test/hlk/)。 如果此列表中包含设备类型的测试类别，则驱动程序发行者应获取驱动程序包的 [WHQL 版本签名](whql-release-signature.md) 。

**注意**   在 Windows Server 2003、Windows XP 和 Windows 2000 上，WHQL 签名的[驱动程序包](driver-packages.md)中的 INF 文件必须使用 *% SystemRoot%/inf/Certclas.inf*中定义的[设备安装程序类](./overview-of-device-setup-classes.md)。 否则，Windows 会将驱动程序包视为无符号。

 

如果通过 WHQL 对驱动程序包进行了数字签名，则可以通过 Windows 更新程序或其他 Microsoft 支持的分发机制来分发该程序包。 WHQL 签署了64位处理器的驱动程序包目录文件，驱动程序发布者还必须在将驱动程序包提交给 WHQL 之前，在内核模式驱动程序文件中 [嵌入签名](embedded-signatures-in-a-driver-file.md) 。

如果 [硬件认证工具包 (HCK) ](/previous-versions/windows/hardware/hck/jj124227(v=vs.85)) 没有适用于你的设备类型的 [测试类别](/windows-hardware/test/hlk/) ，则必须使用以下类型的数字签名在 windows Vista 和更高版本的 windows 上对驱动程序包进行 [发布签名](release-signing-driver-packages.md) ：

-   为了符合内核模式代码签名策略，你只需对驱动程序包的 [目录文件](catalog-files.md)进行签名。 对于启动启动驱动程序，必须在内核模式驱动程序文件中嵌入 SPC 签名，还可以选择对驱动程序包的目录文件进行签名。

-   若要符合 Windows Vista 和更高版本的 windows Vista 和更高版本的 [PnP 设备安装签名32要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md) ，你可以使用 SPC 或 [商业发行版证书](commercial-release-certificate.md) 对内核模式驱动程序包的目录文件进行签名。 后两种签名类型验证驱动程序的真实性和完整性，但不同于 WHQL 版本签名，请不要验证驱动程序的可靠性。

SPC 和商业发布证书统称为 [发布证书](release-certificates.md) ，使用发布证书生成的签名称为 *发布签名*。

有关发布签名要求和过程的详细信息，请参阅 [发布签名驱动程序包](release-signing-driver-packages.md)。

**注意**   若要了解 release 签名驱动程序包中所涉及的步骤，请参阅[如何对驱动程序包进行发布签名](how-to-release-sign-a-driver-package.md)。 本主题提供了版本签名过程的摘要，并通过使用 Windows 驱动程序工具包 (WDK) 中的 *toastpkg.inf* 示例驱动程序包，逐步完成了发布签名的许多示例。

 

