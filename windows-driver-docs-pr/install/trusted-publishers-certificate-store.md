---
title: 受信任的发布者证书存储
description: 受信任的发布者证书存储
ms.assetid: e2fcb0ce-82e3-499a-85b9-76e4e742190e
keywords:
- 驱动程序签名 WDK，受信任的发行者证书存储区
- 受信任的发行者证书存储区 WDK
- WDK 的证书存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e1d715f3222a5468c134e5230b183d8d6374973
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566966"
---
# <a name="trusted-publishers-certificate-store"></a>受信任的发布者证书存储


*受信任的发行者证书存储区*包含有关验证码 （签名） 证书的计算机安装的受信任的发行者信息。 若要测试和调试你[驱动程序包](driver-packages.md)你的公司应在组织中安装用于签署驱动程序包的受信任的发行者证书存储中的验证码证书。 安装运行签名的代码的验证码证书的工作组或组织单位中的每台计算机上。 受信任的发行者证书存储区的名称是*trustedpublisher。*

如果发布服务器的验证码证书的受信任的发行者证书存储中，Windows 安装[驱动程序包](driver-packages.md)的已进行数字签名的证书而不提示用户 (*无提示安装*). 通过将验证码证书安装在受信任的发行者证书存储中，可以自动执行用于内部测试和调试的各种系统上驱动程序包的安装。

**重要**  自动安装的驱动程序包的这种做法只适用于内部系统的建议。 对于分布式组织外部任何驱动程序包应永远不会遵循这种做法。

 

受信任的发行者证书存储区不同于[受信任的根证书颁发机构证书存储区](trusted-root-certification-authorities-certificate-store.md)中，仅*最终实体*可以受信任证书。 例如，如果验证码证书从 CA 已习惯[测试签名](introduction-to-test-signing.md)驱动程序包，将该证书添加到受信任的发行者证书存储区不会配置为受信任此 CA 颁发的所有证书。 每个证书必须单独添加到受信任的发行者证书存储区。

使用组策略将证书分发到网络上的组织单位。 在这种情况下，管理员将证书规则添加到组策略中发布服务器建立信任。 证书规则是在以下 Windows 版本支持的软件限制策略的一部分：

-   Windows Vista 和更高版本的 Windows。

-   Windows Server 2003.

你可以验证码证书到受信任的发行者证书存储区的计算机上通过使用手动安装[ **CertMgr** ](https://msdn.microsoft.com/library/windows/hardware/ff543411)工具。

**请注意**  驱动程序签名验证策略由插需要 CA 的验证码证书具有以前安装在本地计算机受信任的发行者证书存储区的版本。 有关详细信息，请参阅[本地计算机和当前用户证书存储](local-machine-and-current-user-certificate-stores.md)。

 

有关软件限制策略和使用证书规则的详细信息，请参阅 Windows 帮助和支持中心中的信息。 此外，在上找到有关这些主题的详细信息[Microsoft TechNet](https://go.microsoft.com/fwlink/p/?linkid=10111)网站。

有关如何使用组策略部署在企业中的验证码证书的详细信息，请参阅自述文件*Selfsign_readme.htm*，位于*src\\常规\\构建\\driversigning* WDK 的目录。

证书存储区的详细信息，请参阅[代码签名最佳做法](https://go.microsoft.com/fwlink/p/?linkid=68250)网站。

 

 





