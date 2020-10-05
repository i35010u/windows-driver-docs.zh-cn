---
title: 企业 CA 测试证书
description: 企业 CA 测试证书
ms.assetid: c2b075c9-cb85-446d-ac07-65aad5507e62
keywords:
- 企业 CA 测试证书 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9067bcd894b73e867020eda5fea686a0af8d4c63
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732993"
---
# <a name="enterprise-ca-test-certificate"></a>企业 CA 测试证书


*企业 ca 测试证书*是由企业证书颁发机构 (企业 ca) 部署的验证码数字证书。 作为公钥基础结构的一部分，域管理员可以创建企业 CA 来管理正在开发的 [驱动程序包](driver-packages.md) 的企业范围验证码证书。

企业 CA 与 Active Directory 集成，并将证书和证书吊销列表发布到 Active Directory。 企业 CA 使用存储在 Active Directory 中的信息（包括用户帐户和安全组）来批准或拒绝证书申请。

企业 CA 使用证书模板。 颁发证书时，企业 CA 使用证书模板中的信息生成具有该证书类型相应属性的证书。

若要启用自动证书批准和自动用户证书注册，必须将企业 CA 基础结构与 Active Directory 集成。

总而言之，域管理员必须执行以下操作来创建企业 CA，以管理正在开发的 [驱动程序包](driver-packages.md) 的企业范围验证码证书：

-   安装企业 CA。

-    (代码签名) 证书模板创建测试。

-   在 Active Directory 中发布测试证书模板。

-   配置组策略以分发企业 CA 颁发的测试证书。

有关如何配置企业 CA 的详细信息超出了本文档的讨论范围。 有关如何设计公钥基础结构和安装企业 CA 的完整信息，请参阅 [代码签名最佳做法](/windows-hardware/test/hlk/) 网站

Windows Server 2003 部署工具包、Windows Server 2003 帮助和支持中心以及[Microsoft TechNet](https://go.microsoft.com/fwlink/p/?linkid=62647)网站的 "[公钥基础结构](/previous-versions/windows/it-pro/windows-server-2003/cc757327(v=ws.10))" 网页。 TechNet 网站包含有关证书、证书服务和证书模板的信息。

有关将企业 CA 配置为对 [驱动程序包](driver-packages.md) 进行测试签名的信息，请参阅自述文件 *Selfsign_readme.htm*，该文件位于 WDK *的 \\ src general \\ build \\ driversigning* 目录中。

 

