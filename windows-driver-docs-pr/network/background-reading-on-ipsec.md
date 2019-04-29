---
title: 对 IPsec 进行后台读取
description: 对 IPsec 进行后台读取
ms.assetid: b7316027-a66c-4630-88d4-fa3c66f735f8
keywords:
- ESP 受保护的数据包，WDK IPsec 卸载，后台读取
- AH 受保护的数据包，WDK IPsec 卸载，后台读取
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25704a096c6a96693e7a238045a8c8b06050e1a3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367689"
---
# <a name="background-reading-on-ipsec"></a>对 IPsec 进行后台读取

\[IPsec 任务卸载功能已弃用，不应使用。\]




若要理解本部分中，必须了解以下 Rfc 和 IP 安全 Working Group Internet 工程任务组 (IETF) 的发布的草稿中指定的 Internet 协议安全性 (IPsec):

-   [Internet 协议 (RFC 2401) 的安全体系结构](https://go.microsoft.com/fwlink/p/?linkid=9845)

身份验证标头 (AH):

-   [IP 身份验证标头 (RFC 2402)](https://go.microsoft.com/fwlink/p/?linkid=9847)

-   [HMAC-MD5-96 ESP 和 AH (RFC 2403) 内的使用](https://go.microsoft.com/fwlink/p/?linkid=9849)

-   [HMAC-SHA-1-96 ESP 和 AH (RFC 2404) 内的使用](https://go.microsoft.com/fwlink/p/?linkid=9998)

-   [HMAC-MD5 IP 与重播保护 (RFC 2085) 的身份验证](https://go.microsoft.com/fwlink/p/?linkid=9850)

封装安全有效负载 (ESP):

-   [IP 封装安全负载 (ESP) (RFC 2406)](https://go.microsoft.com/fwlink/p/?linkid=9851)

-   [ESP CBC 模式加密算法 (RFC 2451)](https://go.microsoft.com/fwlink/p/?linkid=9853)

-   [ESP DES CBC 密码算法与显式 IV (RFC 2405)](https://go.microsoft.com/fwlink/p/?linkid=9854)

-   [NULL 加密算法和使用 IPsec (RFC 2410)](https://go.microsoft.com/fwlink/p/?linkid=9855)

 

 





