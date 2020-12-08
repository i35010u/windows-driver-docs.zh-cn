---
title: COPP 使用的加密基元
description: COPP 使用的加密基元
keywords:
- 复制保护 WDK COPP，加密
- 视频复制保护 WDK COPP，加密
- COPP WDK DirectX VA，加密
- 受保护的视频 WDK COPP、加密
- 加密 WDK COPP
- 加密 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a72cb0433996438ee83c446062c2452da323185
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832779"
---
# <a name="cryptographic-primitives-used-by-copp"></a>COPP 使用的加密基元


## <span id="ddk_cryptographic_primitives_used_by_copp_gg"></span><span id="DDK_CRYPTOGRAPHIC_PRIMITIVES_USED_BY_COPP_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

COPP 使用以下加密基元：

<span id="Public_key_cryptography"></span><span id="public_key_cryptography"></span><span id="PUBLIC_KEY_CRYPTOGRAPHY"></span>公钥加密  
COPP 要求具有2048位密钥的 RSA 算法用于公钥加密和解密。 有关 RSA 算法的信息，请参阅 [Rsa 实验室](https://go.microsoft.com/fwlink/p/?linkid=70411) 网站。

<span id="Digital_certificates"></span><span id="digital_certificates"></span><span id="DIGITAL_CERTIFICATES"></span>数字证书  
COPP 使用可扩展权限标记语言 (XrML) 数字证书。

<span id="Message_authentication_code__MAC_"></span><span id="message_authentication_code__mac_"></span><span id="MESSAGE_AUTHENTICATION_CODE__MAC_"></span>消息身份验证代码 (MAC)   
COPP 使用单密钥密码块链 (CBC) 模式 MAC (OMAC) 来实现消息的可靠性。 OMAC 基于 (AES) 高级加密标准。 有关 AES 的信息，请参阅 [RSA 实验室](https://go.microsoft.com/fwlink/p/?linkid=70411) 网站。 有关 OMAC 的详细信息，请参阅 [OMAC 算法](https://go.microsoft.com/fwlink/p/?linkid=70417)。

 

 





