---
title: 受信任的发布者证书存储
description: 受信任的发布者证书存储
ms.assetid: e2fcb0ce-82e3-499a-85b9-76e4e742190e
keywords:
- 驱动程序签名 WDK，受信任的发行者证书存储
- 受信任的发布者证书存储 WDK
- 证书存储 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee2c1ee8b3427dedfbb2ad900f4917154578c93a
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732609"
---
# <a name="trusted-publishers-certificate-store"></a>受信任的发布者证书存储


" *受信任的发行者" 证书存储* 包含有关验证 (签名计算机上安装的受信任发布者) 证书的验证码的信息。 为了在你的组织内测试和调试你的 [驱动程序包](driver-packages.md) ，你的公司应该在 "受信任的发行者" 证书存储中安装用于签署驱动程序包的 Authenticode 证书。 在运行签名代码的工作组或组织单位中的每台计算机上安装 Authenticode 证书。 受信任的发布者证书存储区的名称为 *trustedpublisher。*

如果发行者的 Authenticode 证书位于 "受信任的发行者" 证书存储区中，则 Windows 将安装由证书进行数字签名的 [驱动程序包](driver-packages.md) ，而不会提示用户 (*无提示安装*) 。 通过在 "受信任的发行者" 证书存储中安装 Authenticode 证书，你可以在用于内部测试和调试的各种系统上自动安装驱动程序包。

**重要提示**   仅建议你的内部系统对驱动程序包的安装执行这种做法。 对于在组织外部分发的任何驱动程序包，都不应遵循这种做法。

 

"受信任的发行者" 证书存储区不同于 " [受信任的根](trusted-root-certification-authorities-certificate-store.md) 证书颁发机构" 证书存储区，其中只有 *最终实体* 证书可以信任。 例如，如果使用 CA 的验证码证书对驱动程序包进行 [测试签名](introduction-to-test-signing.md) ，将该证书添加到 "受信任的发行者" 证书存储区不会配置此 CA 颁发为受信任的所有证书。 必须将每个证书分别添加到 "受信任的发行者" 证书存储区。

使用组策略将证书分发到网络中的组织单位。 在这种情况下，管理员将证书规则添加到组策略，以在发布服务器中建立信任。 证书规则是以下 Windows 版本支持的软件限制策略的一部分：

-   Windows Vista 和更高版本的 Windows。

-   Windows Server 2003。

可以使用 [**certmgr.msc**](../devtest/certmgr.md) 工具将 Authenticode 证书手动安装到计算机上的 "受信任的发行者" 证书存储中。

**注意**   即插即用使用的驱动程序签名验证策略要求 CA 的验证码证书以前已安装在 "受信任的发布者" 证书存储的 "本地计算机" 版本中。 有关详细信息，请参阅 [Local Machine and Current User Certificate Stores](local-machine-and-current-user-certificate-stores.md)（本地计算机和当前用户证书存储）。

 

有关软件限制策略和使用证书规则的详细信息，请参阅 Windows 帮助和支持中心中的信息。 

有关如何使用组策略在企业中部署 Authenticode 证书证书的详细信息，请参阅自述文件*Selfsign_readme.htm**中的自述 \\ \\ \\ *文件。

有关证书存储的详细信息，请参阅 [代码签名最佳做法](/windows-hardware/test/hlk/) 网站。

