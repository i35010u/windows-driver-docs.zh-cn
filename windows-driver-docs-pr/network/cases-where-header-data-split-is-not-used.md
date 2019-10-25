---
title: 不使用标头数据拆分的情况
description: 不使用标头数据拆分的情况
ms.assetid: e5d3071e-a0d1-4a66-b8aa-6823e737f242
keywords:
- 标头-在未使用时数据拆分 WDK
- 如果未使用，则使用以太网帧拆分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 501d3cf95cdc4e7d927410dff3d0f8e2641480ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835242"
---
# <a name="cases-where-header-data-split-is-not-used"></a>不使用标头数据拆分的情况





本主题概述了标头-数据拆分提供程序不得拆分以太网帧的情况。 若要查看提供程序为支持标头数据拆分而必须满足的最低要求的列表，请参阅[支持标头数据拆分的最低要求](minimum-requirements-for-supporting-header-data-split.md)。

**请注意**  在某些情况下，接收的帧可以在标头数据拆分提供程序要求之外拆分。 即标头-数据拆分要求仅适用于标头-数据拆分提供程序。 在这种情况下，除非第一个 MDL 至少包含与为预测先行大小指定的 NDIS 相同的字节，否则不会将以太网帧拆分为 IP 标头、IPv4 选项、IPsec 标头、IPv6 扩展标头或上层协议标头。

 

所有未拆分的以太网帧必须遵循一般的 NDIS 规则和要求。 例如，接收的[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构中的 MDLs 链中的第一个 MDL 必须包含帧的预测先行部分，或在几乎连续的缓冲区中包含整个以太网帧（取两者中较小者）。 NDIS [\_代\_当前\_预测先行](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-lookahead)oid，设置与 oid 的预测的大小。

标头-数据拆分提供程序：

-   不拆分非 IP 帧。

-   如果框架无法在下列位置之一中拆分，则不拆分它们：在上层协议标头的开头、TCP 负载的开头或 UDP 有效负载的开头。

-   请勿拆分超过配置的最大标头大小的帧，除非可以在[上层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)拆分标头。 有关最大标头大小的详细信息，请参阅[分配标头缓冲区](allocating-the-header-buffer.md)。

-   不要拆分包含 NIC 无法识别的 IPv4 选项的帧。

-   不要拆分包含 NIC 无法识别的 IPv6 扩展标头的帧。

-   请勿拆分包含 NIC 无法识别的 TCP 选项的帧，除非它们可以在 TCP 标头的开头拆分。

 

 





