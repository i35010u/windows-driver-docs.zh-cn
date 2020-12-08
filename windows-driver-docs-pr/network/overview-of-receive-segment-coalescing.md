---
title: 接收段合并概述
description: 接收数据时，微型端口驱动程序、NDIS 和 TCP/IP 必须分别查看每个段的标头信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc13f53b13800d47e304839a9e76a225b32df2d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789655"
---
# <a name="overview-of-receive-segment-coalescing"></a>接收段合并概述


接收数据时，微型端口驱动程序、NDIS 和 TCP/IP 必须分别查看每个段的标头信息。 当收到大量数据时，这会产生大量的开销。 接收段合并 (RSC) 可合并一系列接收的段并将其在一次操作中传递到主机 TCP/IP 堆栈，从而减少此开销，因此，NDIS 和 TCP/IP 只需查看整个序列的一个标头。

RSC 旨在通过以下方式支持合并：

-   不会影响 TCP 拥塞和流控制机制的正常操作。

-   合并数据包而不丢弃 TCP stack 使用的信息。

用于网卡的支持 RSC 的微型端口驱动程序必须：

-   合并段时遵循标准规则集。

-   向主机 TCP/IP 堆栈提供某些带外信息。

以下部分提供了 RSC 的概述。

-   [合并 TCP/IP 段的规则](rules-for-coalescing-tcp-ip-packets.md)
-   [更新合并段的 IP 标头](updating-the-ip-headers-for-coalesced-segments.md)
-   [接收段合并的示例](examples-of-receive-segment-coalescing.md)
-   [指示合并段](indicating-coalesced-segments.md)
-   [终止合并的异常条件](exception-conditions-that-terminate-coalescing.md)

 

 





