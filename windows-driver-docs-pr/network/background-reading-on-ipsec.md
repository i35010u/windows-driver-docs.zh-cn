---
title: 对 IPsec 进行后台读取
description: 对 IPsec 进行后台读取
keywords:
- 受 ESP 保护的数据包 WDK IPsec 卸载，后台读取
- 受 AH 保护的数据包 WDK IPsec 卸载，后台读取
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5d5757c9cc8853c6294d6e3f36acc6bddc6508a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813017"
---
# <a name="background-reading-on-ipsec"></a>对 IPsec 进行后台读取

\[IPsec 任务卸载功能已弃用，不应使用。\]




若要理解此部分，必须了解 internet 工程任务组 (IETF) 的 IP 安全工作组发布的以下 Rfc 和草稿中指定的 Internet 协议安全 (IPsec) ：

-   [Internet 协议的安全体系结构 (RFC 2401) ](https://go.microsoft.com/fwlink/p/?linkid=9845)

AH) 的身份验证标头 (：

-   [IP Authentication 标头 (RFC 2402) ](https://go.microsoft.com/fwlink/p/?linkid=9847)

-   [在 ESP 和 AH 内使用 HMAC-MD5-96 (RFC 2403) ](https://go.microsoft.com/fwlink/p/?linkid=9849)

-   [在 ESP 和 AH 内使用 HMAC-SHA-1-96 (RFC 2404) ](https://go.microsoft.com/fwlink/p/?linkid=9998)

-   [HMAC-具有重播防护 (RFC 2085) 的 MD5 IP 身份验证 ](https://go.microsoft.com/fwlink/p/?linkid=9850)

封装安全有效负载 (ESP) ：

-   [IP 封装安全有效负载 (ESP)  (RFC 2406) ](https://go.microsoft.com/fwlink/p/?linkid=9851)

-   [ESP CBC-Mode 密码算法 (RFC 2451) ](https://go.microsoft.com/fwlink/p/?linkid=9853)

-   [带有显式 IV (RFC 2405) 的 ESP DES CBC 密码算法 ](https://go.microsoft.com/fwlink/p/?linkid=9854)

-   [NULL 加密算法及其用于 IPsec (RFC 2410) ](https://go.microsoft.com/fwlink/p/?linkid=9855)

 

 





