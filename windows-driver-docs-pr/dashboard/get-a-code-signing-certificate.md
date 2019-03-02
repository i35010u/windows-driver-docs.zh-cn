---
title: 获取代码签名证书
description: 获取代码签名证书
ms.assetid: 6CF4111A-C645-40F5-8D45-55F46B3C0740
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d18cf99238bc70da613e6f83496e962eeadba6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518360"
---
# <a name="get-a-code-signing-certificate"></a>获取代码签名证书

在建立合作伙伴中心帐户之前，需要获取代码签名证书以保护数字信息。 此证书是用于建立你的公司对你所提交代码的所有权的接受标准。 它让你可以用数字形式签署 PE 二进制文件，例如 .exe、.cab、.dll、.ocx、.msi、.xpi 和 .xap 文件。

## <a name="step-1-determine-which-type-of-code-signing-certificate-you-need"></a>第 1 步：确定所需的代码签名证书类型

- Microsoft 接受来自为内核模式代码签名注册和授权（作为 Microsoft 受信任的根证书计划的一部分）的合作伙伴的标准代码签名和扩展验证 (EV) 代码签名证书。 如果已有其中一个颁发机构颁发的已批准标准或 EV 证书，则可以使用它建立合作伙伴中心帐户。 如果没有证书，则需要购买一个新证书。

- 下表提供了每个仪表板服务的证书要求的详细信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>仪表板服务/权限</th>
<th>代码签名证书要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bug 管理</p></td>
<td><p>标准或 EV</p></td>
</tr>
<tr class="even">
<td><p>DDC – 驱动程序分发中心</p></td>
<td><p>标准或 EV</p></td>
</tr>
<tr class="odd">
<td><p>设备元数据</p></td>
<td><p>标准或 EV</p></td>
</tr>
<tr class="even">
<td><p>报告数据</p></td>
<td><p>标准或 EV</p></td>
</tr>
<tr class="odd">
<td><p>提交</p></td>
<td><p>标准或 EV</p></td>
</tr>
<tr class="even">
<td><p>WRD – Windows 远程调试</p></td>
<td><p>标准或 EV</p></td>
</tr>
<tr class="odd">
<td><p>LSA</p></td>
<td><p>EV</p></td>
</tr>
<tr class="even">
<td><p>UEFI</p></td>
<td><p>EV</p></td>
</tr>
<tr class="odd">
<td><p>Windows 参考设计</p></td>
<td><p>标准或 EV</p></td>
</tr>
<tr class="even">
<td><p>证明驱动程序签名</p></td>
<td><p>EV</p></td>
</tr>
</tbody>
</table>

> [!NOTE] 
> 今年晚些时候，合作伙伴中心将强制使用提交必需的 EV 证书。

### <a name="code-signing-certificates-for-partner-center"></a>合作伙伴中心的代码签名证书

当前有两种类型的代码签名证书可用：

#### <a name="standard-code-signing"></a>标准代码签名

- 提供标准级别的身份验证

- 需要较短的处理时间以及较低的成本

- 可用于除 LSA 和 UEFI 文件签名服务之外的所有合作伙伴中心服务。

- 在 Windows 10 桌面版（家庭版、专业版、企业版和教育版）中，标准代码签名无法用于内核模式驱动程序。 有关这些更改的详细信息，请参阅[代码签名常见问题](#code-signing-faq)。

#### <a name="extended-validation-ev-code-signing"></a>扩展验证 (EV) 代码签名

- 提供最高级别的身份验证

- 由于扩展了验证过程，因此需要较长的处理时间以及较高的成本

- 可用于所有合作伙伴中心服务，而且是 LSA 和 UEFI 文件签名服务所必需的

- 在 Windows 10 桌面版中，所有内核模式驱动程序都必须由合作伙伴中心签名，并且合作伙伴中心需要 EV 证书。 有关这些更改的详细信息，请参阅[代码签名常见问题](#code-signing-faq)。

## <a name="step-2-buy-a-new-code-signing-certificate"></a>步骤 2：购买新的代码签名证书

如果没有批准的标准或 EV 代码签名证书，可以从下列某个证书颁发机构购买证书。

### <a name="standard-code-signing-certificates"></a>标准代码签名证书

- [购买 Symantec 标准代码签名证书](https://go.microsoft.com/fwlink/?LinkId=393247)

- [购买 Certum 标准代码签名证书](https://go.microsoft.com/fwlink/?linkid=843062)（仅在合作伙伴中心中受支持）

- [购买 Entrust 标准代码签名证书](https://go.microsoft.com/fwlink/?linkid=843067)

- [购买 GlobalSign 标准代码签名证书](https://go.microsoft.com/fwlink/p/?LinkId=620887)

- [购买 Comodo 标准代码签名证书](https://go.microsoft.com/fwlink/?linkid=863206)

- [购买 DigiCert 标准代码签名证书](https://go.microsoft.com/fwlink/?LinkId=393249)

  1. 在“Sysdevs 的 DigiCert 代码签名证书”页上，单击“开始”。

  2. 在“DigiCert 订单”页（步骤 1）上的“代码签名”部分中，单击“代码签名证书”。

  3. 仍在步骤 1 中，向下滚动到“平台”部分，从下拉列表中选择“Microsoft Authenticode”，然后单击“继续”。

  4. 按照 DigiCert 提供的说明购买证书。

### <a name="extended-validation-code-signing-certificatesrequired-for-uefi-kernel-mode-drivers-and-lsa-certifications"></a>扩展验证代码签名证书（对于 UEFI、内核模式驱动程序和 LSA 认证是必需的）

- [购买 Symantec EV 代码签名证书](https://go.microsoft.com/fwlink/?LinkId=393248)

- [购买 Certum EV 代码签名证书](https://go.microsoft.com/fwlink/?linkid=843061)

- [购买 Entrust EV 代码签名证书](https://go.microsoft.com/fwlink/?linkid=843068)

- [购买 GlobalSign EV 代码签名证书](https://go.microsoft.com/fwlink/p/?LinkId=620888)

- [购买 Comodo EV 代码签名证书](https://go.microsoft.com/fwlink/?linkid=863208)

- [购买 DigiCert EV 代码签名证书](https://go.microsoft.com/fwlink/?LinkId=393249)

  1. 在“Sysdevs 的 DigiCert 代码签名证书”页上，单击“开始”。

  2. 在“DigiCert 订单”页上（步骤 1）的“代码签名”部分中，单击“EV 代码签名证书”、填写其余的表单，然后单击“继续”。

  3. 按照 DigiCert 提供的说明购买证书。

## <a name="step-3-retrieve-code-signing-certificates"></a>步骤 3:检索代码签名证书

证书颁发机构验证你的联系信息并批准你的证书购买后，按照他们的指示来检索证书。

> [!NOTE]
> 你必须使用相同的计算机和浏览器来检索你的证书。

## <a name="next-steps"></a>后续步骤

- 如果要设置新的合作伙伴中心帐户，请按照[注册硬件计划](register-for-the-hardware-program.md)中的步骤进行操作。

- 如果已设置合作伙伴中心帐户且需要续订证书，请按照[更新代码签名证书](https://msdn.microsoft.com/library/windows/hardware/update-a-code-signing-certificate)中的步骤进行操作。

## <a name="code-signing-faq"></a>代码签名常见问题

本部分提供有关 Windows 10 代码签名的常见问题的答案。 其他代码签名信息在 Windows 硬件认证博客上提供。

- [Windows 10 中的驱动程序签名更改](http://blogs.msdn.com/b/windows_hardware_certification/archive/2015/04/01/driver-signing-changes-in-windows-10.aspx)
- [Sysdev EV 证书要求更新](http://blogs.msdn.com/b/windows_hardware_certification/archive/2015/10/20/update-on-sysdev-ev-certificate-requirement.aspx)

### <a name="hlk-tested-and-dashboard-signed-drivers"></a>HLK 测试和仪表板签名的驱动程序

- 通过 HLK 测试并经仪表板签名的驱动程序可凭借 Windows 10（包括 Windows Server 版本）在 Windows Vista 上运行。 推荐将此方法用于驱动程序签名，因为它允许将一套过程用于所有操作系统版本。 此外，HLK 测试的驱动程序显示制造商严格测试其硬件，以满足 Microsoft 对于可靠性、安全性、电源效率、可维护性和性能的要求，以便提供出色的 Windows 体验。 这包括兼容行业标准和遵守特定于技术的功能的 Microsoft 规范，有助于确保正确安装、部署、连接和互操作性。 有关 HLK 的详细信息，请参阅 [Windows 硬件兼容性计划](https://docs.microsoft.com/windows-hardware/design/compatibility/index)。

### <a name="windows-10-desktop-attestation-signing"></a>Windows 10 桌面版证明签名

- 使用证明签名的仪表板签名驱动程序仅在 Windows 桌面版和更高版本的 Windows 10 中运行。
- 证明签名的驱动程序仅适用于 Windows 10 桌面版；它不适用于其他版本的 Windows，例如 Windows Server 2016、Windows 8.1 或 Windows 7。
- 证明签名支持 Windows 10 桌面版内核模式和用户模式驱动程序。 尽管用户模式驱动程序无需由适用于 Windows 10 的 Microsoft 进行签名，但相同的证明过程可以同时用于用户和内核模式驱动程序。

### <a name="windows-10-earlier-certificate-transition-signing"></a>Windows 10 早期证书过渡签名

- 不推荐将使用 2015 年 7 月 29 日之后颁发的任何证书进行签名并且带有时间戳的驱动程序用于 Windows 10。
- 使用在 2015 年 7 月 29 日之后到期的任何证书进行签名并且没有时间戳的驱动程序将在 Windows 10 上运行，直到该证书到期。

### <a name="cross-signing-and-sha-256-certificates"></a>交叉签名和 SHA-256 证书

交叉签名介绍了使用 Microsoft 信任的证书颁发机构 (CA) 颁发的证书对某个驱动程序进行签名的过程。 有关详细信息，请参阅[交叉证书概述](https://docs.microsoft.com/windows-hardware/drivers/install/cross-certificates-for-kernel-mode-code-signing)。

- Windows 8 和更高版本均支持 SHA-256。
- 修补后的 Windows 7 支持 SHA-256。 如果需要支持运行 Windows 7 的未修补的设备，则需要使用 SHA-1 证书进行交叉签名，或提交到仪表板以进行签名。 否则，可以使用 SHA-1 或 SHA-2 证书进行交叉签名，或创建 HLK/HCK 提交以进行签名。
- 因为 Windows Vista 不支持 SHA-256，所以需要使用 SHA-1 证书进行交叉签名，或创建 HLK/HCK 提交以进行 Windows Vista 驱动程序签名。
- 在 2015 年 7 月 29 日之前颁发的使用 SHA-256 证书（包括 EV 证书）进行交叉签名的驱动程序将在 Windows 8 和更高版本上运行。 它不会在 Windows Vista 或 Windows Server 2008 上运行。
- 在 2015 年 7 月 29 日之前颁发的使用 SHA-256 证书（包括 EV 证书）进行交叉签名的驱动程序将在 Windows 7 或 Server 2008 R2 上运行，前提是已应用在今年较早时候通过 Windows 更新颁发的修补程序。 有关详细信息，请参阅[适用于 Windows 7 和 Windows Server 2008 R2 的 SHA-2 哈希算法的可用性](https://technet.microsoft.com/library/security/2949927.aspx)和 [Microsoft 安全公告：适用于 Windows 7 和 Windows Server 2008 R2 的 SHA-2 代码签名支持的可用性：2015 年 3 月 10 日](https://support.microsoft.com/kb/3033929)。
- 使用在 2015 年 7 月 29 日前颁发的 SHA-1 证书进行交叉签名的驱动程序可以在从 Windows Vista 到 Windows 10 的所有平台上运行。
- 不推荐将使用在 2015 年 7 月 29 日后颁发的 SHA-1 或 SHA-256 证书进行交叉签名的驱动程序用于 Windows 10。
- 有关移动到 SHA-256 证书的工作的详细信息，请参阅[验证码签名和时间戳的 Windows 强制](http://social.technet.microsoft.com/wiki/contents/articles/32288.windows-enforcement-of-authenticode-code-signing-and-timestamping.aspx)

### <a name="device-guard"></a>Device Guard

- 企业可以实现某项设备保护策略，以使用 Windows 10 企业版修改驱动程序签名要求。 Device Guard 提供企业定义的代码完整性策略，该策略可配置为要求至少一个证明签名的驱动程序。 有关 Device Guard 的详细信息，请参阅 [Device Guard 认证和合规性](https://technet.microsoft.com/library/mt219733.aspx)。

### <a name="windows-server"></a>Windows Server

- 仪表板不会接受证明的设备，并且会筛选用于 Windows Server 2016 的驱动程序签名提交。
- 仪表板仅对设备进行签名，并且筛选成功通过 HLK 测试的驱动程序。
- Windows Server 2016 仅加载成功通过 HLK 测试的仪表板签名的驱动程序。

### <a name="ev-certs"></a>EV 证书

- 截止到 2015 年 10 月 31 日，你的 Sysdev 仪表板帐户必须关联至少一个 EV 证书，才能提交供证明签名的二进制文件，或提交供 HLK 认证的二进制文件。
- 在 2016 年 5 月 1 日前，可以使用 EV 证书或现有标准证书进行签名。 在 2016 年 5 月 1 日后，需要使用 EV 证书才能对提交的 cab 文件进行签名。
- 无需对提交的二进制文件本身进行签名。 仅需要使用 EV 证书对提交的 cab 文件进行签名。

### <a name="os-support-summary"></a>操作系统支持摘要

此表总结了 Windows 的驱动程序签名要求。

|                                    |                                |                                    |                                                                                |
|------------------------------------|--------------------------------|------------------------------------|--------------------------------------------------------------------------------|
|                                    | *已签名的证明仪表板* | *已通过 HLK 测试的已签名仪表板* | *使用在 2015 年 7 月 29 日前颁发的 SHA-1 证书进行交叉签名*         |
| Windows Vista                      | 否                             | 是                                | 是                                                                            |
| Windows 7                          | 否                             | 是                                | 是                                                                            |
| Windows 8/8.1                    | 否                             | 是                                | 是                                                                            |
| Windows 10                         | 是                            | 是                                | 是                                                                            |
| Windows 10 - DG 已启用            | \*配置相关      | \*配置相关          | \*配置相关                                                      |
| Windows Server 2008 R2             | 否                             | 是                                | 是                                                                            |
| Windows Server 2012 R2             | 否                             | 是                                | 是                                                                            |
| Windows Server 2016                | 否                             | 是                                | 是                                                                            |
| Windows Server 2016 – DG 已启用   | \*配置相关      | \*配置相关          | \*配置相关                                                      |
| Windows IoT 企业版             | 是                            | 是                                | 是                                                                            |
| Windows IoT 企业版 - DG 已启用 | \*配置相关      | \*配置相关          | \*配置相关                                                      |
| Windows IoT 核心版(1)                | 是（不需要）             | 是（不需要）                 | 是（交叉签名也适用于 2015 年 7 月 29 日后颁发的证书） |

\*配置相关 - 通过 Windows 10 企业版，组织可以使用 Device Guard 来定义自定义驱动程序签名要求。 有关 Device Guard 的详细信息，请参阅 [Device Guard 认证和合规性](https://technet.microsoft.com/library/mt219733.aspx)。

(1) 制造商生成装有 IoT 核心版的零售产品（即不用于开发用途）需要驱动程序签名。 有关批准的证书颁发机构 (CA) 列表，请参阅[适用于内核模式代码签名的交叉证书](https://docs.microsoft.com/windows-hardware/drivers/install/cross-certificates-for-kernel-mode-code-signing)。 请注意，如果 UEFI 安全启动已启用，则必须对驱动程序进行签名。
