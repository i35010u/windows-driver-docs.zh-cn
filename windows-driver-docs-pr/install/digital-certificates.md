---
title: 数字证书
description: 数字证书
ms.assetid: 90427be5-7b61-4ed6-ab5d-847b64c7dcf0
keywords:
- 数字证书 WDK
- 驱动程序程序包数字证书 WDK
- 包数字证书 WDK
- 数字证书 WDK、 驱动程序包
- 证书 WDK
- WDK、 驱动程序包的证书
- 驱动程序签名 WDK，数字证书
- 签署驱动程序 WDK，数字证书
- 设备安装 WDK，数字证书
- 驱动程序签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 697b2869971ffde81981f6c5e8e0a3433565f050
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542184"
---
# <a name="digital-certificates"></a>数字证书


电子证书绑定到一对特定的公钥和私钥的实体，例如人、 组织或系统。 数字证书可视为验证身份的个人、 系统或组织的电子凭据。

各种类型的数字证书用于多种用途，如下所示：

-   安全多用途 Internet 邮件扩展 (S/MIME) 电子邮件的消息进行签名的数字证书。

-   安全套接字层 (SSL) 和 Internet 协议安全 (IPSec) 数字证书对网络连接进行身份验证。

-   智能卡登录到个人计算机的数字证书。

Windows 代码签名技术使用 X.509 代码签名证书，拥有 Internet 工程任务组 (IETF) 标准。 代码签名证书允许软件发布服务器或分发服务器软件进行数字签名。

证书包含在数字签名并验证签名的原点。 证书所有者的公钥是证书中，用于验证数字签名。 这种做法可以避免无需设置一个中心工具，以便分发证书。 证书所有者私钥单独保留和证书所有者才知道。

软件发布者必须获取证书从证书颁发机构 (CA) 的担保该证书的完整性。 通常情况下，CA 需要软件发布者提供唯一的标识信息。 CA 使用此信息来颁发证书之前进行身份验证请求者的标识。 软件发布者还必须同意遵守由 CA 设置的策略。 如果它们无法实现此目的，CA 可以吊销该证书。

一旦从 CA 获取证书，软件发布者必须将证书存储本地计算机中。 有关此过程的详细信息，请参阅[证书存储区](certificate-stores.md)。

 

 





