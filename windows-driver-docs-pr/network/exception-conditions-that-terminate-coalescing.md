---
title: 终止合并的异常条件
description: 本部分定义接收段合并 (RSC) 功能微型端口驱动程序必须在段上执行的检查，然后才能将其合并。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5c47131d22fde3e2b75124f002f0d438e492a26
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788417"
---
# <a name="exception-conditions-that-terminate-coalescing"></a>终止合并的异常条件


本部分定义接收段合并 (RSC) 功能微型端口驱动程序必须在段上执行的检查，然后才能将其合并。

段必须通过以下两种类型的检查才能合并：

-   检查段中是否存在特定的条件。 例如，TCP 标头中存在 SYN 标志会触发异常，且不会合并段。 下面定义了这些类型的检查。

-   检查是否依赖于检查并关联以前合并的段和当前检查的段中的信息。 例如，检查接收到的段是否为重复确认。 这些类型的检查在 [用于合并 Tcp/ip 段的规则](rules-for-coalescing-tcp-ip-packets.md)中进行定义。

如果检查失败，则会触发异常，而微型端口驱动程序必须终止该 TCP 连接的合并，并按如下所述对待段：

-   检测到异常之前合并的 TCP 段应表示为单个单元。

-   检测到异常之后合并的 TCP 段应表示为一个单独的单元。

**注意**  对于下面的异常7和8，微型端口驱动程序应该从触发异常的段开始恢复合并。

 

接收满足以下任一条件的段必须触发异常：

1.  NIC 中的硬件资源约束阻止了合并。

2.  段的 TCP 或 IP 校验和无效。

3.  段包含其 TCP 标头中的任何 SYN、URG、RST、FIN，如 [RFC 793](https://www.ietf.org/rfc/rfc793.txt)第3.1 节中所定义。 更广泛地说，如果段包含除 PSH 或 ACK 以外的任何标志，则会触发异常。 有关 ECN 标志，请参阅下面的异常8。

4.  段包含一个或多个 tcp 选项，而不是 TCP 时间戳选项。 有关 TCP 时间戳选项的讨论，请参阅 [RFC 1323](https://www.ietf.org/rfc/rfc1323.txt) 。

5.  段包含 IPv4 选项或 IPv6 扩展标头。

6.  段是一个 IPv4 片段。

7.  合并当前接收的段将导致单个合并单元超过最大合法 IP 数据报长度。 此异常需要特殊处理。 有关详细信息，请参阅：

    -   [用于合并 Tcp/ip 数据包的规则](rules-for-coalescing-tcp-ip-packets.md)中的第一个流程图

    -   [Rsc 驱动程序编程注意事项](programming-considerations-for-rsc-drivers.md)中的 "响应 Rsc 统计信息的查询"。

8.  段包含 [RFC 3168](https://www.ietf.org/rfc/rfc3168.txt)中定义的 ECN 标志，该标志满足以下一个或两个条件：

    1.  段在 IP 标头中包含 ECN 字段的值不同的值 (ECT，CE) 。

    2.  此段的 ECN (标志的值不同，TCP 标头中的 ECE 和 CWR) 的值与前一段不同。

 

 





