---
title: RSC 驱动程序的编程注意事项
description: 以下各节描述了在 (RSC) 功能的微型端口驱动程序中实现接收段合并时要考虑的问题。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 208b00862e205004724ff619bf5985ec3adfa218
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805179"
---
# <a name="programming-considerations-for-rsc-drivers"></a>RSC 驱动程序的编程注意事项


以下各节描述了在 (RSC) 功能的微型端口驱动程序中实现接收段合并时要考虑的问题。

-   [响应 RSC 统计信息的查询](#responding-to-queries-for-rsc-statistics)
-   [转发的 TCP 数据包](#forwarded-tcp-packets)
-   [RSC 对轻型筛选器和 MUX 中间驱动程序的支持](#rsc-support-for-lightweight-filters-and-mux-intermediate-drivers)
-   [Windows 筛选平台 (WFP) 检查和标注驱动程序](#windows-filtering-platform-wfp-inspection-and-callout-drivers)

## <a name="responding-to-queries-for-rsc-statistics"></a>响应 RSC 统计信息的查询


NDIS、过量驱动程序和用户模式应用程序使用 [oid \_ TCP \_ RSC \_ statistics](./oid-tcp-rsc-statistics.md) OID 来获取微型端口适配器的 RSC 统计信息。 支持 RSC 的微型端口驱动程序必须支持此 OID。

## <a name="forwarded-tcp-packets"></a>转发的 TCP 数据包


小型端口驱动程序不应在 TCP 数据包中的段上执行 RSC，而不应在另一个接口上将其转发。

主机 TCP/IP 堆栈将在启用转发的任何接口上禁用 RSC。 弱主机转发不影响 RSC。

## <a name="rsc-support-for-lightweight-filters-and-mux-intermediate-drivers"></a>RSC 对轻型筛选器和 MUX 中间驱动程序的支持


所有 NDIS 6.30 轻型筛选器驱动程序都必须支持大于链接最大传输单位 (MTU) 的接收数据包。 有关段大小限制的详细信息，请参阅 [指示合并段](indicating-coalesced-segments.md)。

如果主机堆栈中的任何轻型筛选器驱动程序或 MUX 中间驱动程序是 NDIS 6.20 或更低版本，NDIS 将在接口上禁用 RSC。

MUX 中间驱动程序可以在接口上禁用 RSC，即使接口的 NDIS 版本为6.30 或更高版本。

## <a name="windows-filtering-platform-wfp-inspection-and-callout-drivers"></a>Windows 筛选平台 (WFP) 检查和标注驱动程序


WFP 标注驱动程序通过在一个或多个内核模式筛选层将自定义标注函数添加到筛选器引擎来提供附加的筛选功能。 标注支持深度检查和数据包以及流修改。

WFP 标注驱动程序可以支持对大于链接 MTU 的支持接收数据包的处理。  (有关数据包大小限制的详细信息，请参阅 [跟踪和指示合并段](./indicating-coalesced-segments.md)。 ) 此类 WFP 标注驱动程序应执行以下操作：

-   在注册期间选择加入，以处理大数据包。

-   设置 [**FWPS \_ CALLOUT2**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout2_) 结构的参考页中指定的标注驱动程序标志。

无论何时注册了未选择处理大数据包的标注驱动程序，WFP 都将在注册的上下文中通知 TCP/IP。 在处理此通知的过程中，TCP/IP 将在接口上禁用 RSC。

如果在标注注册过程中存在活动 TCP 流量，TCP/IP 将通知 WFP。 在禁用 RSC 之前，WFP 会延迟调用已注册的筛选器。 这将保护来自大数据包的标注驱动程序。

 

