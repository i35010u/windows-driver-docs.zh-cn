---
title: 内置标注标识符
description: 本部分介绍内置标注标识符。
ms.assetid: c0200388-1e79-41b9-890c-ce0034b329d8
keywords:
- 内置标注标识符网络驱动程序
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: af466e48be6c13231bf9b76e389e5ff8a53ded14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542655"
---
# <a name="built-in-callout-identifiers"></a>内置标注标识符

每个表示的 guid Windows 筛选平台中内置的标注的标识符。 这些标识符定义，如下所示。

> [!NOTE]
> 标注标识符结尾处的 V4 和 v6 上后缀指示标注是否适用于 IPv4 网络堆栈或 IPv6 网络堆栈。

| 内置标注标识符 | 标注说明 |
| --- | --- |
| <p>FWPM_CALLOUT_IPSEC_INBOUND_TRANSPORT_V4</p><p>FWPM_CALLOUT_IPSEC_INBOUND_TRANSPORT_V6</p> | 验证应通过传输模式安全关联到达每个接收的数据包到达安全。 此标注是适用于传输层。 |
| <p>FWPM_CALLOUT_IPSEC_OUTBOUND_TRANSPORT_V4</p><p>FWPM_CALLOUT_IPSEC_OUTBOUND_TRANSPORT_V6</p> | IPsec 中，指示必须保护传输模式安全关联上的出站流量。 此标注是适用于传输层。 |
| <p>FWPM_CALLOUT_IPSEC_INBOUND_TUNNEL_V4</p><p>FWPM_CALLOUT_IPSEC_INBOUND_TUNNEL_V6</p> | 验证应通过隧道模式安全关联到达每个接收的数据包到达安全。 此标注是适用于传输层。 |
| <p>FWPM_CALLOUT_IPSEC_OUTBOUND_TUNNEL_V4</p><p>FWPM_CALLOUT_IPSEC_OUTBOUND_TUNNEL_V6</p> | IPsec 中，指示必须保护通过隧道模式安全关联的出站流量。 此标注是适用于传输层。 |
| <p>FWPM_CALLOUT_IPSEC_FORWARD_INBOUND_TUNNEL_V4</p><p>FWPM_CALLOUT_IPSEC_FORWARD_INBOUND_TUNNEL_V6</p> | 验证应通过隧道模式安全关联到达每个接收的数据包到达安全。 此标注是适用于正向的层。 |
| <p>FWPM_CALLOUT_IPSEC_FORWARD_OUTBOUND_TUNNEL_V4</p><p>FWPM_CALLOUT_IPSEC_FORWARD_OUTBOUND_TUNNEL_V6</p> | IPsec 中，指示必须保护通过隧道模式安全关联的出站流量。 此标注是适用于正向的层。 |
| <p>FWPM_CALLOUT_IPSEC_INBOUND_INITIATE_SECURE_V4</p><p>FWPM_CALLOUT_IPSEC_INBOUND_INITIATE_SECURE_V6</p> | 验证要安全地到达每个传入连接是。 此标注是适用于 ALE 接受层。 |
| <p>FWPM_CALLOUT_IPSEC_ALE_CONNECT_V4</p><p>FWPM_CALLOUT_IPSEC_ALE_CONNECT_V6</p> | 适用于客户端应用程序的 IPsec 策略修饰符。 |
| <p>FWPM_CALLOUT_WFP_TRANSPORT_LAYER_V4_SILENT_DROP</p><p>FWPM_CALLOUT_WFP_TRANSPORT_LAYER_V6_SILENT_DROP</p> | 以无提示方式删除所有 TCP 不具有侦听终结点的传入数据包。 此标注是适用于入站的传输层。 |
| <p>FWPM_CALLOUT_TCP_CHIMNEY_CONNECT_LAYER_V4</p><p>FWPM_CALLOUT_TCP_CHIMNEY_CONNECT_LAYER_V6</p> | 启用或禁用 TCP 烟囱卸载的每个传出连接。 |
| <p>FWPM_CALLOUT_TCP_CHIMNEY_ACCEPT_LAYER_V4</p><p>FWPM_CALLOUT_TCP_CHIMNEY_ACCEPT_LAYER_V6</p> | 启用或禁用 TCP 烟囱卸载的每个传入的连接。 |

