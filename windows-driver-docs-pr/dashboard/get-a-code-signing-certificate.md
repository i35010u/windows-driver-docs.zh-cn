---
title: 获取代码签名证书
description: 获取代码签名证书
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d925cdf9f2546734ed8971b2d3732d2ca2eb554
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800367"
---
# <a name="get-a-code-signing-certificate"></a>获取代码签名证书

在建立合作伙伴中心帐户之前，需要获取代码签名证书以保护数字信息。 此证书是用于建立你的公司对你所提交代码的所有权的接受标准。 它让你可以用数字形式签署 PE 二进制文件，例如 .exe、.cab、.dll、.ocx、.msi、.xpi 和 .xap 文件。

## <a name="step-1-obtain-an-ev-certificate"></a>步骤 1：获取 EV 证书

- Microsoft 需要为内核模式代码签名注册和授权（作为 Microsoft 受信任的根证书计划的一部分）的合作伙伴提供的扩展验证 (EV) 代码签名证书。 如果已有其中一个颁发机构颁发的已批准 EV 证书，则可以使用它建立合作伙伴中心帐户。 如果没有证书，则需要购买一个新证书。

## <a name="step-2-buy-a-new-code-signing-certificate"></a>步骤 2：购买新的代码签名证书

如果没有批准的 EV 代码签名证书，可以从下列某个证书颁发机构购买证书。

### <a name="extended-validation-code-signing-certificates"></a>扩展验证代码签名证书。

- [购买 SSL.com EV 代码签名证书](https://www.ssl.com/certificates/ev-code-signing/)

- [购买 Certum EV 代码签名证书](https://shop.certum.eu/data-safety/code-signing-certificates/certum-ev-code-sigining.html)

- [购买 Entrust EV 代码签名证书](https://www.entrustdatacard.com/products/digital-signing-certificates/code-signing-certificates)

- [购买 GlobalSign EV 代码签名证书](https://go.microsoft.com/fwlink/p/?LinkId=620888)

- [购买 Sectigo（以前称为 Comodo）EV 代码签名证书](https://go.microsoft.com/fwlink/?linkid=863208)

- [购买 DigiCert EV 代码签名证书](https://www.digicert.com/order/order-1.php)

## <a name="step-3-retrieve-code-signing-certificates"></a>步骤 3:检索代码签名证书

证书颁发机构验证你的联系信息并批准你的证书购买后，按照他们的指示来检索证书。

> [!NOTE]
> 你必须使用相同的计算机和浏览器来检索你的证书。

## <a name="step-4-add-the-certificates-to-your-account-on-partner-center"></a>步骤 4：在合作伙伴中心，将证书添加到你的帐户

有关分步说明，请参阅[添加或更新代码签名证书](update-a-code-signing-certificate.md)。

## <a name="next-steps"></a>后续步骤

- 如果要设置新的合作伙伴中心帐户，请按照[注册硬件计划](register-for-the-hardware-program.md)中的步骤进行操作。

- 如果已设置合作伙伴中心帐户且需要续订证书，请按照[添加或更新代码签名证书](update-a-code-signing-certificate.md)中的步骤进行操作。

## <a name="code-signing-faq"></a>代码签名常见问题

本部分提供有关 Windows 10 代码签名的常见问题的答案。 其他代码签名信息在 Windows 硬件认证博客上提供。

- [Windows 10 中的驱动程序签名更改](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/Driver-Signing-changes-in-Windows-10/ba-p/364859)
- [Windows 10 的版本 1607 中的驱动程序签名更改](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/Driver-Signing-changes-in-Windows-10-version-1607/ba-p/364894)
- [Sysdev EV 证书要求更新](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/Update-on-Sysdev-EV-Certificate-requirement/ba-p/364879)

### <a name="hlk-tested-and-dashboard-signed-drivers"></a>HLK 测试和仪表板签名的驱动程序

- 通过 HLK 测试并经仪表板签名的驱动程序可凭借 Windows 10（包括 Windows Server 版本）在 Windows Vista 上运行。 推荐将此方法用于驱动程序签名，因为它允许将一套过程用于所有操作系统版本。 此外，HLK 测试的驱动程序显示制造商严格测试其硬件，以满足 Microsoft 对于可靠性、安全性、电源效率、可维护性和性能的要求，以便提供出色的 Windows 体验。 这包括兼容行业标准和遵守特定于技术的功能的 Microsoft 规范，有助于确保正确安装、部署、连接和互操作性。 有关 HLK 的详细信息，请参阅 [Windows 硬件兼容性计划](/windows-hardware/design/compatibility/index)。

### <a name="windows-10-desktop-attestation-signing"></a>Windows 10 桌面版证明签名

- 使用证明签名的仪表板签名驱动程序仅在 Windows 桌面版和更高版本的 Windows 10 中运行。
- 证明签名的驱动程序仅适用于 Windows 10 桌面版，不适用于其他版本的 Windows，例如 Windows 7、Windows 8.1 或 Windows Server 2016 及更高版本。
- 证明签名支持 Windows 10 桌面版内核模式和用户模式驱动程序。

### <a name="windows-10-earlier-certificate-transition-signing"></a>Windows 10 早期证书过渡签名

- 下面的内容仅适用于 Windows 10 1803 及更低版本。  从 Windows 10 1809 开始，这些将不再适用。
- 不推荐将使用 2015 年 7 月 29 日之后颁发的任何证书进行签名并且带有时间戳的驱动程序用于 Windows 10。
- 使用在 2015 年 7 月 29 日之后到期的任何证书进行签名并且没有时间戳的驱动程序将在 Windows 10 上运行，直到该证书到期。

### <a name="cross-signing-and-sha-256-certificates"></a>交叉签名和 SHA-256 证书

交叉签名介绍了使用 Microsoft 信任的证书颁发机构 (CA) 颁发的证书对某个驱动程序进行签名的过程。 有关详细信息，请参阅[交叉证书概述](../install/cross-certificates-for-kernel-mode-code-signing.md)。

- Windows 8 和更高版本均支持 SHA-256。
- 修补后的 Windows 7 支持 SHA-256。 如果需要支持运行 Windows 7 的未修补的设备，则需要使用 SHA-1 证书进行交叉签名，或提交到仪表板以进行签名。 否则，可以使用 SHA-1 或 SHA-2 证书进行交叉签名，或创建 HLK/HCK 提交以进行签名。
- 因为 Windows Vista 不支持 SHA-256，所以需要使用 SHA-1 证书进行交叉签名，或创建 HLK/HCK 提交以进行 Windows Vista 驱动程序签名。
- 在 2015 年 7 月 29 日之前颁发的使用 SHA-256 证书（包括 EV 证书）进行交叉签名的驱动程序将在 Windows 8 和更高版本上运行。 它不会在 Windows Vista 或 Windows Server 2008 上运行。
- 在 2015 年 7 月 29 日之前颁发的使用 SHA-256 证书（包括 EV 证书）进行交叉签名的驱动程序将在 Windows 7 或 Server 2008 R2 上运行，前提是已应用在今年较早时候通过 Windows 更新颁发的修补程序。 有关详细信息，请参阅[适用于 Windows 7 和 Windows Server 2008 R2 的 SHA-2 哈希算法的可用性](/security-updates/SecurityAdvisories/2014/2949927)和 [Microsoft 安全公告：适用于 Windows 7 和 Windows Server 2008 R2 的 SHA-2 代码签名支持的可用性：2015 年 3 月 10 日](https://support.microsoft.com/help/3033929/microsoft-security-advisory-availability-of-sha-2-code-signing-support)。
- 使用在 2015 年 7 月 29 日前颁发的 SHA-1 证书进行交叉签名的驱动程序可以在从 Windows Vista 到 Windows 10 的所有平台上运行。
- 不推荐将使用在 2015 年 7 月 29 日后颁发的 SHA-1 或 SHA-256 证书进行交叉签名的驱动程序用于 Windows 10。
- 有关移动到 SHA-256 证书的工作的详细信息，请参阅[验证码签名和时间戳的 Windows 强制](https://social.technet.microsoft.com/wiki/contents/articles/32288.windows-enforcement-of-authenticode-code-signing-and-timestamping.aspx)

### <a name="windows-defender-application-control"></a>Microsoft Defender 应用程序控制

- 企业可实现一项策略，使用 Windows 10 企业版修改驱动程序签名要求。 Microsoft Defender 应用程序控制 (WDAC) 提供企业定义的代码完整性策略，该策略可配置为要求至少一个证明签名的驱动程序。 有关 WDAC 的详细信息，请参阅 [关于 Microsoft Defender 应用程序控制部署过程的计划和入门](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)。

### <a name="windows-server"></a>Windows Server

- Windows Server 2016 及更高版本将不接受证明的设备和筛选驱动程序签名提交。
- 仪表板仅对设备进行签名，并且筛选成功通过 HLK 测试的驱动程序。
- Windows Server 2016 及更高版本将只加载已成功通过 HLK 测试的仪表板签名的驱动程序。

### <a name="ev-certs"></a>EV 证书

- 截止到 2015 年 10 月 31 日，你的硬件开发人员中心仪表板帐户必须关联至少一个 EV 证书，才能提交供证明签名的二进制文件，或提交供 HLK 认证的二进制文件。
- 必须对提交的二进制文件本身进行签名。

### <a name="os-support-summary"></a>操作系统支持摘要

此表总结了 Windows 的驱动程序签名要求。

| 版本 | *已签名的证明仪表板* | *已通过 HLK 测试的已签名仪表板* | *使用在 2015 年 7 月 29 日前颁发的 SHA-1 证书进行交叉签名* |
|--|--|--|--|
| Windows Vista | 否 | 是 | 是 |
| Windows 7 | 否 | 是 | 是 |
| Windows 8/8.1 | 否 | 是 | 是 |
| Windows 10 | 是 | 是 | 否（截至 Windows 10 1809） |
| Windows 10 - DG 已启用 | \*配置相关 | \*配置相关 | \*配置相关 |
| Windows Server 2008 R2 | 否 | 是 | 是 |
| Windows Server 2012 R2 | 否 | 是 | 是 |
| Windows Server >= 2016 | 否 | 是 | 是 |
| Windows Server >= 2016 – DG 已启用 | \*配置相关 | \*配置相关 | \*配置相关 |
| Windows IoT 企业版 | 是 | 是 | 是 |
| Windows IoT 企业版 - DG 已启用 | \*配置相关 | \*配置相关 | \*配置相关 |
| Windows IoT 核心版(1) | 是（不需要） | 是（不需要） | 是（交叉签名也适用于 2015 年 7 月 29 日后颁发的证书） |

\*配置从属 - 通过 Windows 10 企业版，组织可使用 Microsoft Defender 应用程序控制 (WDAC) 来定义自定义签名要求。 有关 WDAC 的详细信息，请参阅 [关于 Microsoft Defender 应用程序控制部署过程的计划和入门](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)。

(1) 制造商生成装有 IoT 核心版的零售产品（即不用于开发用途）需要驱动程序签名。 有关批准的证书颁发机构 (CA) 列表，请参阅[适用于内核模式代码签名的交叉证书](../install/cross-certificates-for-kernel-mode-code-signing.md)。 请注意，如果 UEFI 安全启动已启用，则必须对驱动程序进行签名。
