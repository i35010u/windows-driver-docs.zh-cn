---
title: 完全 TCP 卸载
description: 完全 TCP 卸载
keywords:
- TCP 卸载 WDK 网络
- 烟囱卸载 WDK 网络，完全
- 卸载处理 WDK 网络
- 完整的 TCP 卸载 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a64d11ca36d0aedd1523129f1c94d5e9da4e0f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825499"
---
# <a name="full-tcp-offload"></a>完全 TCP 卸载





NDIS 6.0 引入了用于完整 TCP 卸载的体系结构。 此体系结构称为 "烟囱卸载" 体系结构，因为它在应用程序和支持卸载的 NIC 之间提供了一个称为 "烟囱" 的直接连接。 烟囱使 NIC 能够为卸载的连接执行 TCP 处理，包括维护协议状态。

烟囱卸载体系结构减少了网络密集型应用程序的主机网络处理。 这使得联网的应用程序可以更有效地进行扩展，同时也减少了端到端的延迟。 承载应用程序所需的服务器较少，并且服务器能够使用完全以太网带宽。

TCP 烟囱卸载一个或多个 TCP 连接的所有 TCP 处理。 在 (SAR) 上卸载分段和重组，并卸载可确保可靠连接的处理 (例如，确认处理和 TCP 重新传输计时器) ，并减少中断负载，从而获得主要性能提升。

**注意**  Windows Vista 操作系统继续支持早期版本的操作系统中可用的单个 TCP 任务卸载。 这些任务可以在未通过烟囱卸载的连接上被卸载。 支持卸载的 NIC 应同时支持烟囱卸载和任务卸载。 这种 NIC 提供最高程度的卸载优化。

 

有关 NDIS 6.0 和更高版本中 TCP 烟囱卸载的信息，请参阅 [NDIS TCP 烟囱卸载](/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)。

 

