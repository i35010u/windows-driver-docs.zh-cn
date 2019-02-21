---
title: 终止合并的异常条件
description: 本部分将定义一个接收段合并 (RSC) 的检查-支持的微型端口驱动程序必须执行段上之前可合并。
ms.assetid: 6294541A-AF32-46CF-81AB-5855EA440053
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 891a482918833a430df81481c3f097ac75261603
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540409"
---
# <a name="exception-conditions-that-terminate-coalescing"></a>终止合并的异常条件


本部分将定义一个接收段合并 (RSC) 的检查-支持的微型端口驱动程序必须执行段上之前可合并。

段必须通过这两个以下类型的检查之前可合并：

-   检查存在的段中的某一特定条件。 例如，TCP 标头中的 SYN 标志存在会触发异常并不会合并段。 检查这些类型定义如下。

-   依赖于检查并将以前合并的段和检查当前段中的信息相关联的检查。 例如，检查是否已接收的段是一个重复确认属于此类别的检查中。 检查这些类型中定义[规则合并 TCP/IP 段](rules-for-coalescing-tcp-ip-packets.md)。

如果检查失败，异常触发，并且微型端口驱动程序必须终止该 TCP 连接的合并和处理段，如下所示：

-   检测到异常之前已合并的 TCP 段应指示作为单个单元。

-   后检测到异常都会合并的 TCP 段应表示为一个单独的单元。

**请注意**  对于 7 和 8 下面的例外，微型端口驱动程序应继续合并开头触发了异常的段。

 

接收符合以下条件的任意一个段必须触发了异常：

1.  NIC 中的硬件资源约束防止合并。

2.  段具有无效的 TCP 或 IP 校验和。

3.  段包含的任意 SYN、 URG、 RST、 FIN TCP 标头中的第 3.1 节中定义[RFC 793](http://www.ietf.org/rfc/rfc793.txt)。 更广泛地说，如果该段包含 PSH 或确认以外的任何标志，则应触发异常。 ECN 标记，请参阅异常 8 下面。

4.  段包含一个或多个 TCP 选项，而不是 TCP 时间戳选项。 请参阅[RFC 1323](http://www.ietf.org/rfc/rfc1323.txt) TCP 时间戳选项的讨论。

5.  段包含 IPv4 选项或 IPv6 扩展标头。

6.  段是一个 IPv4 片段。

7.  合并当前接收的段将会导致要为超过最大的法律 IP 数据报长度的单个合并的单元。 此异常需要特殊处理。 有关详细信息，请参阅：

    -   中的第一个流程图[合并 TCP/IP 数据包的规则](rules-for-coalescing-tcp-ip-packets.md)

    -   "响应查询的 RSC 统计信息"中的[RSC 驱动程序的编程注意事项](programming-considerations-for-rsc-drivers.md)。

8.  段包含 ECN 标记中定义[RFC 3168](http://www.ietf.org/rfc/rfc3168.txt)，满足一个或两个以下条件：

    1.  段比上一个段的 IP 标头中包含 ECN 字段 （ECT，CE） 的不同值。

    2.  段具有比上一个段的 TCP 标头中的 ECN 标记 （ECE 和 CWR） 不同的值。

 

 





