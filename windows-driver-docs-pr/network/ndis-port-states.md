---
title: NDIS 端口状态
description: NDIS 端口状态
ms.assetid: bb13edd2-815b-488a-b36c-21a48809a143
keywords:
- 端口 WDK NDIS，状态
- NDIS 端口 WDK，状态
- 状态 WDK NDIS 端口
- 身份验证状态 WDK NDIS 端口
- 链接状态 WDK NDIS 端口
- 初始化状态 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04ca4a1df62f3f4b65a29dae0aa35972f353db86
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826915"
---
# <a name="ndis-port-states"></a>NDIS 端口状态





NDIS 端口具有操作状态，包括在[**NDIS\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)结构中指定的初始化状态和状态。 端口状态适合以下类别：

<a href="" id="initialization-states"></a>初始化状态  
NDIS 端口初始化状态与启动初始化和即插即用（PnP）事件关联。 当 NDIS 或微型端口驱动程序首次分配端口时，端口将处于已*分配状态*。 在 NDIS 或微型端口驱动程序激活端口之后，端口将处于 "已*激活" 状态*。 非活动端口无法发送或接收数据、进行状态指示、接收 OID 请求或启动 PnP 事件。

<a href="" id="link-states"></a>链接状态  
NDIS 端口链接状态类似于与微型端口适配器关联的链接状态以及在[**NDIS\_link\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构中指定的链接状态。 端口链接状态指示媒体链接连接状态和链接速度。 端口的链接状态可能与关联的微型端口适配器的链接状态不同。

<a href="" id="authentication-states"></a>身份验证状态  
NDIS 端口身份验证状态指示端口是否受控制（需要授权）、数据传输方向（发送、接收或两者），以及端口的授权状态（已授权或未经授权）。 如果端口不受控制，则会忽略经过身份验证且未通过身份验证的状态。

微型端口驱动程序可以激活端口，或使用 PnP 事件停用端口。 有关激活和停用端口的详细信息，请参阅[激活 Ndis 端口](activating-an-ndis-port.md)和[停用 ndis 端口](deactivating-an-ndis-port.md)。

过量驱动程序使用[oid\_GEN\_端口\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)OID 获取在[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**PortNumber**成员中指定的端口的当前状态。 NDIS 处理此 OID，微型端口驱动程序不会收到此 OID 查询。

支持 NDIS 端口的微型端口驱动程序必须使用[**NDIS\_状态\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)指示，以指明 NDIS 端口状态的更改。 微型端口驱动程序必须在[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**PortNumber**成员中设置端口号。

NDIS 和过量驱动程序使用[OID\_代\_端口\_AUTHENTICATION\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-authentication-parameters)OID 设置 NDIS 端口的当前身份验证状态。 支持 NDIS 端口的微型端口驱动程序必须支持此 OID。

 

 





