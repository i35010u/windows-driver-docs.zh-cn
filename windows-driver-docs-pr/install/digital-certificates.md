---
title: 数字证书
description: 数字证书
keywords:
- 数字证书 WDK
- 驱动程序包数字证书 WDK
- 打包数字证书 WDK
- 数字证书 WDK，驱动程序包
- 证书 WDK
- 证书 WDK，驱动程序包
- 驱动程序签名 WDK，数字证书
- 对驱动程序进行签名 WDK，数字证书
- 设备安装 WDK，数字证书
- 驱动程序签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9716d1f94bd5b0016e5b22b1748e21859cddc66a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782769"
---
# <a name="digital-certificates"></a>数字证书


数字证书将实体（例如个人、组织或系统）绑定到特定的公钥和私钥对。 数字证书可以看作是验证个人、系统或组织身份的电子凭据。

各种类型的数字证书用于多种目的，例如：

-   安全多用途 Internet 邮件扩展 (S/MIME) 数字证书来签署电子邮件。

-   安全套接字层 (SSL) 和 Internet 协议安全 (IPSec) 用于对网络连接进行身份验证的数字证书。

-   用于登录到个人计算机的智能卡数字证书。

Windows 代码签名技术使用 x.509 代码签名证书，该证书是 Internet 工程任务组 (IETF) 的一种标准。 代码签名证书允许软件发行者或分发服务器对软件进行数字签名。

证书包含在数字签名中，用于验证签名的来源。 证书所有者的公钥在证书中，用于验证数字签名。 这种做法无需设置用于分发证书的中央设施。 证书所有者的私钥是单独保存的，只是证书所有者知道的。

软件发行者必须从证书颁发机构获取证书， (CA) ，该证书可提供证书的完整性。 通常，CA 要求软件发行者提供唯一的标识信息。 CA 在颁发证书之前，使用此信息对请求者的身份进行身份验证。 软件发行者还必须同意遵守 CA 设置的策略。 如果无法执行此操作，CA 可以吊销证书。

从 CA 获取证书后，软件发布者必须将证书存储在本地计算机上。 有关此过程的详细信息，请参阅 [证书存储](certificate-stores.md)。

 

 





