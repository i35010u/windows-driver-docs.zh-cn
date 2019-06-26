---
title: IHV 端口监视器中的自动配置
description: IHV 端口监视器中的自动配置
ms.assetid: c41c8502-902a-448c-8f96-fb196e68ee6e
keywords:
- IHV 端口监视器自动配置 WDK 打印机
- 自动配置 WDK 打印机，IHV 端口监视器
- 打印机自动配置 WDK 打印机，IHV 端口监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b52d57bef2f3bf0171a564a0d2123ea751a97986
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370466"
---
# <a name="autoconfiguration-in-an-ihv-port-monitor"></a>IHV 端口监视器中的自动配置


想要开发端口监视器 IHV 必须设计为支持自动配置。 IHV 端口监视器中的自动配置为提供支持，请遵循以下准则：

-   实现[ **SendRecvBidiDataFromPort** ](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))函数，并将放置在此函数的地址**pfnSendRecvBidiDataFromPort**隶属[**MONITOR2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/ns-winsplp-_monitor2)结构。

-   支持[bidi 通信架构](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)。

-   支持 bidi 通知。

IHV 不需要开发端口监视器，如果在 box 支持部门就足够了。 (有关详细信息，请参阅[自动配置的现成支持](in-box-support-for-autoconfiguration.md)。)请注意，仅适用于标准 TCP/IP 端口监视器和 Web Services for Devices (WSD) 端口监视器提供内置支持。 想要提供自动配置为本地打印机必须提供端口监视器的 Ihv。

 

 




