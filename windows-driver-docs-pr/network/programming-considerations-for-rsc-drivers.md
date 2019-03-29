---
title: RSC 驱动程序的编程注意事项
description: 以下各节介绍实现接收段合并 (RSC) 时需考虑的问题-支持的微型端口驱动程序。
ms.assetid: 03FDD557-3918-408A-BD79-64CD52BDD43A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b914f68a10322564c788ef0596a3011f1d1f6e9b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566002"
---
# <a name="programming-considerations-for-rsc-drivers"></a>RSC 驱动程序的编程注意事项


以下各节介绍实现接收段合并 (RSC) 时需考虑的问题-支持的微型端口驱动程序。

-   [RSC 统计信息的响应的查询](#responding-to-queries-for-rsc-statistics)
-   [转发的 TCP 数据包](#forwarded-tcp-packets)
-   [RSC 支持轻型筛选器和 MUX 中间驱动程序](#rsc-support-for-lightweight-filters-and-mux-intermediate-drivers)
-   [Windows 筛选平台 (WFP) 检查和标注驱动程序](#windows-filtering-platform-wfp-inspection-and-callout-drivers)

## <a name="responding-to-queries-for-rsc-statistics"></a>RSC 统计信息的响应的查询


NDIS、 基础驱动程序和用户模式应用程序使用[OID\_TCP\_RSC\_统计信息](https://msdn.microsoft.com/library/windows/hardware/hh451929)要获取的微型端口适配器 RSC 统计信息的 OID。 Rsc 功能的微型端口驱动程序必须支持此 OID。

## <a name="forwarded-tcp-packets"></a>转发的 TCP 数据包


微型端口驱动程序不应执行 RSC 上不适用于主机，但需要转发出另一个接口上的 TCP 数据包中的段。

主机 TCP/IP 堆栈将禁用已启用转发任何接口上的 RSC。 转发的弱主机不会影响 RSC。

## <a name="rsc-support-for-lightweight-filters-and-mux-intermediate-drivers"></a>RSC 支持轻型筛选器和 MUX 中间驱动程序


轻型筛选器驱动程序必须支持的所有 NDIS 6.30 都接收大于链接最大传输单元 (MTU) 的数据包。 有关段大小限制的详细信息，请参阅[，该值指示合并段](indicating-coalesced-segments.md)。

NDIS 将 RSC 接口上的则禁用任何轻型筛选器驱动程序或 MUX 主机堆栈中的中间驱动程序 NDIS 6.20 或较低。

MUX 中间驱动程序可能会禁用 RSC 上一个接口，即使接口的 NDIS 版本 6.30 或更高版本。

## <a name="windows-filtering-platform-wfp-inspection-and-callout-drivers"></a>Windows 筛选平台 (WFP) 检查和标注驱动程序


WFP 标注驱动程序通过将自定义标注函数添加到筛选器引擎在一个或多个内核模式筛选层提供附加的筛选功能。 标注支持深度检测和数据包，以及流修改。

WFP 标注驱动程序可能支持的支持处理接收大于链接 MTU 的数据包。 (有关数据包大小限制的详细信息，请参阅[跟踪和，该值指示合并段](https://msdn.microsoft.com/library/windows/hardware/jj853326)。)此类 WFP 标注驱动程序应执行以下操作：

-   选择以处理大型数据包在注册过程。

-   按指定的参考页中设置的标注驱动程序标志[ **FWPS\_CALLOUT2** ](https://msdn.microsoft.com/library/windows/hardware/hh439700)结构。

每当注册未选择加入以处理大的数据包的标注驱动程序，WFP 会通知登记的上下文中的 TCP/IP。 作为处理此通知的一部分，TCP/IP 将禁用 RSC 接口上。

如果在标注注册期间活动的 TCP 流量，TCP/IP 会通知 WFP。 WFP 会延迟调用已注册的筛选器，直到禁用 RSC。 这将防止大型数据包标注驱动程序。

 

 





