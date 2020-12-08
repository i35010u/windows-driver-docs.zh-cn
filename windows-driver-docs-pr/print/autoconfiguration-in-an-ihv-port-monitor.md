---
title: IHV 端口监视器中的自动配置
description: IHV 端口监视器中的自动配置
keywords:
- IHV 端口监视器自动配置 WDK 打印机
- 自动配置 WDK 打印机，IHV 端口监视器
- 打印机自动配置 WDK 打印机，IHV 端口监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bceab0c5fa507100d043fb594e601fe264331d44
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836077"
---
# <a name="autoconfiguration-in-an-ihv-port-monitor"></a>IHV 端口监视器中的自动配置


打算开发端口监视器的 IHV 必须将其设计为支持自动配置。 若要为 IHV 端口监视器中的自动配置提供支持，请遵循以下准则：

-   实现 [**SendRecvBidiDataFromPort**](/previous-versions/ff562071(v=vs.85))函数，并将此函数的地址放置在 [**MONITOR2**](/windows-hardware/drivers/ddi/winsplp/ns-winsplp-_monitor2)结构的 **pfnSendRecvBidiDataFromPort** 成员中。

-   支持 [双向通信架构](./bidi-communications-schema-reference.md)。

-   支持双向通知。

如果内置支持就已足够，则不需要使用 IHV 来开发端口监视器。  (详细信息，请参阅 [自动配置的内置支持](in-box-support-for-autoconfiguration.md)。 ) 请注意，仅为标准 tcp/ip 端口监视器和用于设备的 Web 服务 (WSD) 端口监视器提供内置支持。 打算为本地打印机提供自动配置的 Ihv 必须提供端口监视器。

 

