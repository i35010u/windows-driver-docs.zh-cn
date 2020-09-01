---
title: 不使用标头数据拆分的情况
description: 不使用标头数据拆分的情况
ms.assetid: e5d3071e-a0d1-4a66-b8aa-6823e737f242
keywords:
- 标头-在未使用时数据拆分 WDK
- 如果未使用，则使用以太网帧拆分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a86bf4e75bc255cb0a39edeb298d26fbbe0a6cd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213987"
---
# <a name="cases-where-header-data-split-is-not-used"></a>不使用标头数据拆分的情况





本主题概述了标头-数据拆分提供程序不得拆分以太网帧的情况。 若要查看提供程序为支持标头数据拆分而必须满足的最低要求的列表，请参阅 [支持标头数据拆分的最低要求](minimum-requirements-for-supporting-header-data-split.md)。

**注意**   在某些情况下，接收的帧可以在标头数据拆分提供程序要求之外拆分。 即标头-数据拆分要求仅适用于标头-数据拆分提供程序。 在这种情况下，除非第一个 MDL 至少包含与为预测先行大小指定的 NDIS 相同的字节，否则不会将以太网帧拆分为 IP 标头、IPv4 选项、IPsec 标头、IPv6 扩展标头或上层协议标头。

 

所有未拆分的以太网帧必须遵循一般的 NDIS 规则和要求。 例如，接收的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构中的 MDLs 链中的第一个 MDL 必须包含帧的预测先行部分或整个以太网帧 (在几乎连续的缓冲区中，这两个小) 。 NDIS 设置具有 [OID 生成 \_ \_ 当前 \_ 预测先行](./oid-gen-current-lookahead.md) oid 的预测的大小。

标头-数据拆分提供程序：

-   不拆分非 IP 帧。

-   如果框架无法在下列位置之一中拆分，则不拆分它们：在上层协议标头的开头、TCP 负载的开头或 UDP 有效负载的开头。

-   请勿拆分超过配置的最大标头大小的帧，除非可以在 [上层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)拆分标头。 有关最大标头大小的详细信息，请参阅 [分配标头缓冲区](allocating-the-header-buffer.md)。

-   不要拆分包含 NIC 无法识别的 IPv4 选项的帧。

-   不要拆分包含 NIC 无法识别的 IPv6 扩展标头的帧。

-   请勿拆分包含 NIC 无法识别的 TCP 选项的帧，除非它们可以在 TCP 标头的开头拆分。

 

