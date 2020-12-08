---
title: 内置的标注标识符
description: 本部分介绍内置标注标识符。
keywords:
- 内置标注标识符网络驱动程序
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55ede266efcfda28691f02b49c165e4a70af55f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802367"
---
# <a name="built-in-callout-identifiers"></a>内置的标注标识符

内置于 Windows 筛选平台中的标注的标识符由 GUID 表示。 这些标识符的定义如下。

> [!NOTE]
> 标注标识符末尾的 V4 和 V6 后缀指示标注是用于 IPv4 网络堆栈还是 IPv6 网络堆栈。

| 内置标注标识符 | 标注说明 |
| --- | --- |
| <p>FWPM_CALLOUT_IPSEC_INBOUND_TRANSPORT_V4</p><p>FWPM_CALLOUT_IPSEC_INBOUND_TRANSPORT_V6</p> | 验证每个接收到的数据包是否应通过传输模式安全关联。 此标注适用于传输层。 |
| <p>FWPM_CALLOUT_IPSEC_OUTBOUND_TRANSPORT_V4</p><p>FWPM_CALLOUT_IPSEC_OUTBOUND_TRANSPORT_V6</p> | 向 IPsec 指明必须通过传输模式安全关联保护的出站流量。 此标注适用于传输层。 |
| <p>FWPM_CALLOUT_IPSEC_INBOUND_TUNNEL_V4</p><p>FWPM_CALLOUT_IPSEC_INBOUND_TUNNEL_V6</p> | 验证每个接收到的数据包是否应通过隧道模式安全关联。 此标注适用于传输层。 |
| <p>FWPM_CALLOUT_IPSEC_OUTBOUND_TUNNEL_V4</p><p>FWPM_CALLOUT_IPSEC_OUTBOUND_TUNNEL_V6</p> | 向 IPsec 指明必须通过隧道模式安全关联保护的出站流量。 此标注适用于传输层。 |
| <p>FWPM_CALLOUT_IPSEC_FORWARD_INBOUND_TUNNEL_V4</p><p>FWPM_CALLOUT_IPSEC_FORWARD_INBOUND_TUNNEL_V6</p> | 验证每个接收到的数据包是否应通过隧道模式安全关联。 此标注适用于正向层。 |
| <p>FWPM_CALLOUT_IPSEC_FORWARD_OUTBOUND_TUNNEL_V4</p><p>FWPM_CALLOUT_IPSEC_FORWARD_OUTBOUND_TUNNEL_V6</p> | 向 IPsec 指明必须通过隧道模式安全关联来保护的出站流量。 此标注适用于正向层。 |
| <p>FWPM_CALLOUT_IPSEC_INBOUND_INITIATE_SECURE_V4</p><p>FWPM_CALLOUT_IPSEC_INBOUND_INITIATE_SECURE_V6</p> | 验证每个应该安全到达的传入连接是否已安全到达。 此标注适用于 ALE 接受层。 |
| <p>FWPM_CALLOUT_IPSEC_ALE_CONNECT_V4</p><p>FWPM_CALLOUT_IPSEC_ALE_CONNECT_V6</p> | 将 IPsec 策略修饰符应用于客户端应用程序。 |
| <p>FWPM_CALLOUT_WFP_TRANSPORT_LAYER_V4_SILENT_DROP</p><p>FWPM_CALLOUT_WFP_TRANSPORT_LAYER_V6_SILENT_DROP</p> | 以无提示方式删除 TCP 没有侦听终结点的所有传入数据包。 此标注适用于入站传输层。 |
| <p>FWPM_CALLOUT_TCP_CHIMNEY_CONNECT_LAYER_V4</p><p>FWPM_CALLOUT_TCP_CHIMNEY_CONNECT_LAYER_V6</p> | 为每个传出连接启用或禁用 TCP 烟囱卸载。 |
| <p>FWPM_CALLOUT_TCP_CHIMNEY_ACCEPT_LAYER_V4</p><p>FWPM_CALLOUT_TCP_CHIMNEY_ACCEPT_LAYER_V6</p> | 启用或禁用每个传入连接的 TCP 烟囱卸载。 |

