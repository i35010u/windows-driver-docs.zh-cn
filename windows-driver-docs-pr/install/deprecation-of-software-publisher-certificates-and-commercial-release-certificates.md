---
title: 弃用软件发行者证书、商业发布证书和商业测试证书
description: 弃用软件发行者证书、商业发布证书和商业测试证书
ms.assetid: eafa4e20-94c5-49d6-a192-2fc7c9f1e64g
keywords:
- 受信任的根证书颁发机构证书存储 WDK
- 受信任的发布者证书存储 WDK
ms.date: 08/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 13d142c5826d77bc4a1be46137de3b7afaefd942
ms.sourcegitcommit: 55171d00a4d0776ffbea40ab421f765c5432fcaa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2019
ms.locfileid: "69011927"
---
# <a name="deprecation-of-software-publisher-certificates-commercial-release-certificates-and-commercial-test-certificates"></a>弃用软件发行者证书、商业发布证书和商业测试证书

[Microsoft 受信任的根程序](https://docs.microsoft.com/security/trusted-root/program-requirements)不再支持具有内核模式签名功能的根证书。

有关策略要求, 请参阅[Windows 10 内核模式代码签名要求](https://docs.microsoft.com/security/trusted-root/program-requirements#f-windows-10-kernel-mode-code-signing-kmcs-requirements)。

在过期之前, 具有内核模式代码签名功能的现有[交叉签名根证书](cross-certificates-for-kernel-mode-code-signing.md)将继续工作。
因此, 链接回这些根证书的所有[软件发行者证书](software-publisher-certificate.md)、[商业发布证书](commercial-release-certificate.md)和[商业测试证书](commercial-test-certificate.md)也会在同一计划中无效。  若要对驱动程序进行签名, 请首先[注册 Windows 硬件开发人员中心计划](https://docs.microsoft.com/windows-hardware/drivers/dashboard/register-for-the-hardware-program)。

## <a name="frequently-asked-questions"></a>常见问题解答
* [可信交叉证书的到期计划是什么？](#what-is-the-expiration-schedule-of-the-trusted-cross-certificates)
* [交叉签名证书的哪些替代选项可用于测试驱动程序？](#what-alternatives-to-cross-signed-certificates-are-available-for-testing-drivers)
* [现有的签名驱动程序包会发生什么情况？](#what-will-happen-to-my-existing-signed-driver-packages)
* [是否有方法可以运行生产驱动程序包, 而无需将其公开给 Microsoft？](#is-there-a-way-to-run-production-driver-packages-without-exposing-it-to-microsoft)
* [驱动程序包的每个新版本是否需要重新提交给硬件开发人员中心？](#does-every-new-production-version-of-a-driver-package-need-to-be-signed-by-microsoft)
* [我们是否会继续在2021后用现有的第三方颁发的证书对非驱动程序代码进行签名？](#will-we-continue-to-be-able-to-sign-non-driver-code-with-our-existing-3rd-party-issued-certificates-after-2021)
* [我是否能够继续使用我的 EV 证书来签署提交给硬件开发人员中心的证书？](#will-i-be-able-to-continue-using-my-ev-certificate-for-signing-submissions-to-hardware-dev-center)
* [如何实现知道我的签名证书是否会受到这些过期的影响？](#how-do-i-know-if-my-signing-certificate-will-be-impacted-by-these-expirations)
* [如何将 Microsoft 测试签名自动用于生成过程？](#how-can-we-automate-microsoft-test-signing-to-work-with-our-build-processes)
* [从2021开始, Microsoft 是否是生产内核模式代码签名的唯一提供程序？](#starting-in-2021-will-microsoft-be-the-sole-provider-of-production-kernel-mode-code-signatures)
* [硬件开发人员中心不提供适用于 Windows XP 的驱动程序签名, 如何让我的驱动程序在 XP 中运行？](#hardware-dev-center-doesnt-provide-driver-signing-for-windows-xp-how-can-i-have-my-drivers-run-in-xp)

### <a name="what-is-the-expiration-schedule-of-the-trusted-cross-certificates"></a>可信交叉证书的到期计划是什么？

根据以下计划, 大多数交叉签名根证书将在2021后过期:

|公用名| 过期日期|
|-----------|---------------|
|VeriSign 类3公共主证书颁发机构-G5       |2/22/2021|
|thawte 主根 CA                                             |2/22/2021|
|GeoTrust 主证书颁发机构                           |2/22/2021|
|GeoTrust 主证书颁发机构-G3                      |2/22/2021|
|thawte 主根 CA-G3                                        |2/22/2021|
|VeriSign 通用根证书颁发机构                    |2/22/2021|
|TC TrustCenter Class 2 CA II                                       |4/11/2021|
|COMODO RSA 证书颁发机构                                 |4/11/2021|
|UTN-USERFirst-对象                                               |4/11/2021|
|DigiCert 有保障的 ID 根 CA                                        |4/15/2021|
|DigiCert 高确定性 EV 根 CA                                 |4/15/2021|
|DigiCert 全局根 CA                                            |4/15/2021|
|Entrust.net 证书颁发机构 (2048)                         |4/15/2021|
|GlobalSign 根 CA                                                 |4/15/2021|
|中转 Daddy 根证书颁发机构-G2                           |4/15/2021|
|Starfield 根证书颁发机构-G2                          |4/15/2021|
|NetLock Arany (Class 黄金) Fotanúsítvány                           |4/15/2021|
|NetLock Arany (Class 黄金) Fotanúsítvány                           |4/15/2021|
|NetLock Platina (类白金) Fotanúsítvány                     |4/15/2021|
|安全通信 RootCA1                                     |4/15/2021|
|StartCom 证书颁发机构                                   |4/15/2021|
|Certum 可信网络 CA                                          |4/15/2021|
|COMODO ECC 证书颁发机构                                 |4/11/2021|

### <a name="what-alternatives-to-cross-signed-certificates-are-available-for-testing-drivers"></a>交叉签名证书的哪些替代选项可用于测试驱动程序？

可以使用以下替代方法:

- [MakeCert 进程](makecert-test-certificate.md)
- [WHQL 测试签名计划](whql-test-signature-program.md)
- [企业 CA 流程](enterprise-ca-test-certificate.md)

若要使用这些选项, 必须启用[TESTSIGNING](the-testsigning-boot-configuration-option.md)。 有关详细信息, 请参阅[在开发和测试过程中为驱动程序签名](signing-drivers-during-development-and-test.md)。

### <a name="what-will-happen-to-my-existing-signed-driver-packages"></a>现有的签名驱动程序包会发生什么情况？ 

只要驱动程序包在中间证书的到期日期之前有时间戳, 它们将继续工作。

### <a name="is-there-a-way-to-run-production-driver-packages-without-exposing-it-to-microsoft"></a>是否有方法可以运行生产驱动程序包, 而无需将其公开给 Microsoft？ 

不可以, 所有生产驱动程序包都必须提交给 Microsoft 并签署。 

### <a name="does-every-new-production-version-of-a-driver-package-need-to-be-signed-by-microsoft"></a>驱动程序包的每个新生产版本是否需要由 Microsoft 签名？

是的, 每次重建生产级驱动程序包时, 必须由 Microsoft 签名。

### <a name="will-we-continue-to-be-able-to-sign-non-driver-code-with-our-existing-3rd-party-issued-certificates-after-2021"></a>我们是否会继续在2021后用现有的第三方颁发的证书对非驱动程序代码进行签名？

是的, 这些证书在过期之前将继续工作。 使用这些证书签名的代码将只能在用户模式下运行, 并且将不允许在内核中运行, 除非它具有有效的 Microsoft 签名。

### <a name="will-i-be-able-to-continue-using-my-ev-certificate-for-signing-submissions-to-hardware-dev-center"></a>我是否能够继续使用我的 EV 证书来签署提交给硬件开发人员中心的证书？  

是的, 你可以使用有效的 EV 证书对硬件开发人员中心的提交包进行签名, 但由 EV 证书签名的驱动程序包将不再在证书的到期日期之后验证。 

### <a name="how-do-i-know-if-my-signing-certificate-will-be-impacted-by-these-expirations"></a>如何实现知道我的签名证书是否会受到这些过期的影响？ 

如果交叉证书链以结尾`Microsoft Code Verification Root`, 则签名证书会受到影响。 

若要查看交叉证书链, 请`signtool verify /v /kp <mydriver.sys>`运行。 例如：

![[查找交叉证书链]](images/signtoolcrosssigexample.png)

### <a name="how-can-we-automate-microsoft-test-signing-to-work-with-our-build-processes"></a>如何将 Microsoft 测试签名自动用于生成过程？

你的生成过程可以调用[硬件开发人员中心 API](../dashboard/dashboard-api.md)。 

有关显示用法的示例, 请参阅[Surface 开发人员中心经理](https://github.com/Microsoft/SDCM)存储库。

### <a name="starting-in-2021-will-microsoft-be-the-sole-provider-of-production-kernel-mode-code-signatures"></a>从2021开始, Microsoft 是否是生产内核模式代码签名的唯一提供程序？ 

是。

### <a name="hardware-dev-center-doesnt-provide-driver-signing-for-windows-xp-how-can-i-have-my-drivers-run-in-xp"></a>硬件开发人员中心不提供适用于 Windows XP 的驱动程序签名, 如何让我的驱动程序在 XP 中运行？

仍可使用第三方颁发的代码签名证书对驱动程序进行签名。 但是, 对驱动程序进行签名的证书必须导入到`Local Computer Trusted Publishers`目标计算机上的证书存储中。 有关详细信息, 请参阅[受信任的发布者证书存储](trusted-publishers-certificate-store.md)。

## <a name="related-information"></a>相关信息

* [注册硬件计划](https://docs.microsoft.com/windows-hardware/drivers/dashboard/register-for-the-hardware-program)
* [软件发行者证书](software-publisher-certificate.md)
* [商业发布证书](commercial-release-certificate.md)
* [商业测试证书](commercial-test-certificate.md)
