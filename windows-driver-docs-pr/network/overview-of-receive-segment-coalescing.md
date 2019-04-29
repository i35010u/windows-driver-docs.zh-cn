---
title: 接收段合并概述
description: 在接收数据时，微型端口驱动程序、 NDIS 和 TCP/IP 必须所有考虑每个段的标头信息单独。
ms.assetid: 1E9BC335-BB62-415B-B242-D63672A4E406
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ade849ed2c05e014f0b8c9ca380c7efbeecd520
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365742"
---
# <a name="overview-of-receive-segment-coalescing"></a>接收段合并概述


在接收数据时，微型端口驱动程序、 NDIS 和 TCP/IP 必须所有考虑每个段的标头信息单独。 正在接收大量数据，这将创建大量的开销。 接收的段合并 (RSC) 通过合并一系列接收的段和传递到主机 TCP/IP 堆栈在一个操作中，以便在整个序列的一个标头仅查找 NDIS 和 TCP/IP，需要减少此开销。

RSC 旨在支持合并的方式的：

-   不会干扰 TCP 的拥塞和流控制机制的正常操作。

-   将数据包合并而无需放弃使用 TCP 堆栈的信息。

网络卡的 rsc 功能的微型端口驱动程序必须：

-   合并段时，请遵循标准的规则集。

-   提供某些带外信息对主机 TCP/IP 堆栈。

以下部分提供 RSC 的概述。

-   [规则合并 TCP/IP 段](rules-for-coalescing-tcp-ip-packets.md)
-   [有关合并的段更新 IP 标头](updating-the-ip-headers-for-coalesced-segments.md)
-   [示例接收段合并](examples-of-receive-segment-coalescing.md)
-   [指示合并段](indicating-coalesced-segments.md)
-   [终止合并的异常条件](exception-conditions-that-terminate-coalescing.md)

 

 





