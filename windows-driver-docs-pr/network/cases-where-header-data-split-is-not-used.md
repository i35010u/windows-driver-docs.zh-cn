---
title: 不使用标头数据拆分的情况
description: 不使用标头数据拆分的情况
ms.assetid: e5d3071e-a0d1-4a66-b8aa-6823e737f242
keywords:
- 标头数据拆分 WDK，如果不使用
- 如果不使用拆分 WDK 网络的以太网帧
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c09a64994118e165413f086281dd0250655638a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368335"
---
# <a name="cases-where-header-data-split-is-not-used"></a>不使用标头数据拆分的情况





本主题提供的标头数据在何处拆分提供程序的用例概述必须不会拆分以太网帧。 有关提供程序必须满足的最低要求的列表，以支持标头数据拆分，请参阅[最低要求支持标头数据拆分](minimum-requirements-for-supporting-header-data-split.md)。

**请注意**  某些情况下，可以将接收的帧拆分外部标头数据拆分提供商的要求。 即，标头数据拆分要求仅适用于标头数据拆分提供程序。 在这些情况下，永远不会将拆分 IP 标头、 IPv4 选项、 IPsec 标头、 IPv6 扩展标头或大写层协议标头，中间的以太网帧除非第一个 MDL NDIS 为预测先行大小指定为包含至少多少个字节。

 

所有不会拆分的以太网帧必须遵循的一般 NDIS 规则和要求。 例如，在收到 MDLs 链中的第一个 MDL [ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构必须包含在帧的预测先行一部分或整个以太网帧 （两者中较小）中的几乎连续的缓冲区。 NDIS 设置与预期的大小[OID\_代\_当前\_预测先行](https://msdn.microsoft.com/library/windows/hardware/ff569574)OID。

标头数据拆分提供程序：

-   不拆分非 IP 帧。

-   如果它们不能在这些位置之一的拆分不拆分帧： upper 层协议标头的开头、 TCP 有效负载，开头或 UDP 负载的开头。

-   不会拆分将超过最大配置标头大小，除非可以处拆分标头的帧[的右上层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。 有关最大标头大小的详细信息，请参阅[分配标头缓冲区](allocating-the-header-buffer.md)。

-   不会拆分包含 NIC 无法识别的 IPv4 选项的帧。

-   不会拆分包含 NIC 无法识别的 IPv6 扩展标头的帧。

-   不会拆分包含 NIC 无法识别除非 TCP 标头的开始处拆分的 TCP 选项的帧。

 

 





