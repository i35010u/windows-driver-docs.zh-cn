---
title: 商业发布证书
description: 商业发布证书
ms.assetid: bc3966e6-a7e4-4c5c-8dcf-9b95e61ba9b1
keywords:
- 商业版本发布证书 WDK
- 目录文件 WDK 驱动程序签名，商业版本发布证书
- 公开发布的版本驱动程序签名 WDK，商业版本发布证书
- 释放签名 WDK，商业版本发布证书
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1053059165e9d4f678e655d36edce3e781ec9313
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576231"
---
# <a name="commercial-release-certificate"></a>商业发布证书


一个*商业版本发布证书*指的是发布服务器将从属于 Microsoft 根证书计划的受信任的第三方的商业证书颁发机构 (CA) 获取数字证书。 GTE 和 VeriSign，Inc.是此类 CAs 的两个示例。 CA，则此计划的成员验证的标识和授权的应聘者，然后颁发证书申请人用来签名的驱动程序。 签名过程具有发布者的标识标记的驱动程序，并可以用于验证该驱动程序签名后未被修改。

出于安全原因，不应使用数字证书将用来为版本签名驱动程序测试签名驱动程序。 你应获取单独使用版本签名证书和用于测试签名的数字证书。 有关如何管理电子证书的信息，请参阅[管理的数字签名或代码签名密钥](managing-the-digital-signature-or-code-signing-keys.md)。

按照有关如何获取并你将用于签署驱动程序的计算机上安装发布证书的 CA 提供的说明。

有关如何从 CA 获取数字证书的详细信息，请参阅[Microsoft 根证书程序成员](https://go.microsoft.com/fwlink/p/?linkid=74266)网站。

 

 





