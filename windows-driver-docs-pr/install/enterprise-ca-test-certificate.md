---
title: 企业 CA 测试证书
description: 企业 CA 测试证书
ms.assetid: c2b075c9-cb85-446d-ac07-65aad5507e62
keywords:
- 企业 CA 测试证书 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8031a46471c7c777058646ef11437d34ba26f00d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566599"
---
# <a name="enterprise-ca-test-certificate"></a>企业 CA 测试证书


*企业 CA 测试证书*是整个企业内部署的企业证书颁发机构 (企业 CA) 的验证码数字证书。 公钥基础结构的一部分，作为域管理员可以创建企业 CA 来管理的企业级验证码证书[驱动程序包](driver-packages.md)正在开发。

企业 CA 与 Active Directory 集成，并将发布证书和证书吊销列表到 Active Directory。 企业 CA 使用存储在 Active Directory，包括用户帐户和安全组，以批准或拒绝证书申请的信息。

企业 CA 使用证书模板。 颁发证书时，企业 CA 使用证书模板中的信息生成具有该证书类型相应属性的证书。

如果你想要启用自动的证书批准和自动用户证书注册，必须与 Active Directory 集成的企业 CA 基础结构。

总之，域管理员必须执行以下操作来创建企业 CA 来管理的企业级验证码证书[驱动程序包](driver-packages.md)正在开发：

-   安装企业 CA。

-   创建测试 （代码签名） 的证书模板。

-   在 Active Directory 中发布的测试证书模板。

-   配置组策略分发企业 CA 颁发的测试证书。

如何配置企业 CA 的详细的信息不在此文档的范围。 有关如何设计公钥基础结构和安装企业 CA 的完整信息，请参阅[代码签名最佳做法](https://go.microsoft.com/fwlink/p/?linkid=68250)网站，

Windows Server 2003 部署工具包、 Windows Server 2003 帮助和支持中心，并[公共密钥基础结构](https://go.microsoft.com/fwlink/p/?linkid=62645)的网页[Microsoft TechNet](https://go.microsoft.com/fwlink/p/?linkid=62647)网站。 TechNet 网站包含有关证书、 证书服务和证书模板的信息。

了解如何配置测试登录到企业 CA[驱动程序包](driver-packages.md)自述文件中还提供了*Selfsign_readme.htm*，其位于*src\\常规\\构建\\driversigning* WDK 的目录。

 

 





