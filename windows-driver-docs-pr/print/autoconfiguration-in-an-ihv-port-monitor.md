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
ms.openlocfilehash: 2591eaa8bbd8b465a65e07d1911ba462d8d4fe88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350752"
---
# <a name="autoconfiguration-in-an-ihv-port-monitor"></a>IHV 端口监视器中的自动配置


想要开发端口监视器 IHV 必须设计为支持自动配置。 IHV 端口监视器中的自动配置为提供支持，请遵循以下准则：

-   实现[ **SendRecvBidiDataFromPort** ](https://msdn.microsoft.com/library/windows/hardware/ff562071)函数，并将放置在此函数的地址**pfnSendRecvBidiDataFromPort**隶属[**MONITOR2** ](https://msdn.microsoft.com/library/windows/hardware/ff557532)结构。

-   支持[bidi 通信架构](https://msdn.microsoft.com/library/windows/hardware/ff545175)。

-   支持 bidi 通知。

IHV 不需要开发端口监视器，如果在 box 支持部门就足够了。 (有关详细信息，请参阅[自动配置的现成支持](in-box-support-for-autoconfiguration.md)。)请注意，仅适用于标准 TCP/IP 端口监视器和 Web Services for Devices (WSD) 端口监视器提供内置支持。 想要提供自动配置为本地打印机必须提供端口监视器的 Ihv。

 

 




