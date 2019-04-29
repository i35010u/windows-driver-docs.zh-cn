---
title: COPP 使用的加密基元
description: COPP 使用的加密基元
ms.assetid: a14f6f4c-75fd-41a3-93f8-86c9908a2343
keywords:
- 复制保护 WDK COPP，加密
- 视频复制保护 WDK COPP，加密
- COPP WDK DirectX VA 加密
- 受保护视频 WDK COPP 加密
- 加密 WDK COPP
- 加密 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81c95ae5a9ecde73889c686ab64c7880957c931f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371489"
---
# <a name="cryptographic-primitives-used-by-copp"></a>COPP 使用的加密基元


## <span id="ddk_cryptographic_primitives_used_by_copp_gg"></span><span id="DDK_CRYPTOGRAPHIC_PRIMITIVES_USED_BY_COPP_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。

COPP 使用以下加密基元：

<span id="Public_key_cryptography"></span><span id="public_key_cryptography"></span><span id="PUBLIC_KEY_CRYPTOGRAPHY"></span>公钥加密  
COPP 需要带有公钥加密和解密的 2,048 位密钥的 RSA 算法。 有关 RSA 算法的信息，请参阅[RSA Laboratories](https://go.microsoft.com/fwlink/p/?linkid=70411)网站。

<span id="Digital_certificates"></span><span id="digital_certificates"></span><span id="DIGITAL_CERTIFICATES"></span>数字证书  
COPP 使用可扩展权限标记语言 (XrML) 数字证书。

<span id="Message_authentication_code__MAC_"></span><span id="message_authentication_code__mac_"></span><span id="MESSAGE_AUTHENTICATION_CODE__MAC_"></span>消息验证代码 (MAC)  
COPP 使用一个密钥加密块链接 (CBC)-消息真实性 MAC (OMAC) 模式。 OMAC 基于在高级加密标准 (AES)。 AES 有关的信息，请参阅[RSA Laboratories](https://go.microsoft.com/fwlink/p/?linkid=70411)网站。 有关 OMAC 详细信息，请参阅[OMAC 1 算法](https://go.microsoft.com/fwlink/p/?linkid=70417)。

 

 





