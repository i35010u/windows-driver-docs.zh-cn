---
title: 完整的 TCP 卸载
description: 完整的 TCP 卸载
ms.assetid: a940617a-b848-430d-8da1-acd946feba1b
keywords:
- TCP 卸载 WDK 网络
- 烟囱卸载 WDK 网络、 完整
- 卸载处理 WDK 网络
- 完整的 TCP 卸载 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a588b090ccadb36e2adca78c4124a38ead0d7b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542687"
---
# <a name="full-tcp-offload"></a>完整的 TCP 卸载





NDIS 6.0 引入了一种体系结构以进行完整的 TCP 卸载。 此体系结构称为"烟囱卸载"体系结构因为它提供了一个名为"烟囱，"的直接连接的应用程序之间支持卸载的 nic。 烟囱启用要执行 TCP 处理对于卸载连接，包括维护协议状态的 NIC。

烟囱卸载体系结构可降低网络密集型应用程序的主机网络处理。 这样，联网的应用程序更高效地缩放，同时还可降低端到端延迟。 需要使用更少的服务器来托管应用程序，并且服务器能够使用完整的以太网带宽。

TCP 烟囱卸载所有 TCP 处理对于一个或多个 TCP 连接。 从卸载分段和重组 （特别行政区） 卸载处理，以确保可靠的连接 （例如，确认处理和 TCP 重新传输计时器），并减少中断加载获取主要性能提升。

**请注意**  Windows Vista 操作系统继续支持早期版本的操作系统中单个 TCP 任务卸载。 可以在连接不通过烟囱卸载都会卸载这些任务。 支持卸载的 NIC 都应支持这两个烟囱卸载和任务将卸载。 此类 NIC 提供最高程度的卸载优化。

 

有关 TCP 烟囱卸载 NDIS 6.0 及更高版本的信息，请参阅[NDIS TCP 烟囱卸载](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)。

 

 





