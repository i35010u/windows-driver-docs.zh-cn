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
ms.openlocfilehash: 831188b8fba144458b373d54b2411f76ac2df4f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354958"
---
# <a name="ndis-port-states"></a>NDIS 端口状态





NDIS 端口的操作包括初始化状态和中指定的状态的状态[ **NDIS\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_state)结构。 端口状态分为以下类别：

<a href="" id="initialization-states"></a>初始化状态  
NDIS 端口的初始化状态是与启动初始化关联的即插即用 (PnP) 事件。 NDIS 或微型端口驱动程序首先会分配一个端口，端口时，在*分配状态*。 NDIS 或微型端口驱动程序将激活一个端口后，该端口处于*激活状态*。 非活动端口无法发送或接收数据、 进行状态指示，接收 OID 请求或启动即插即用事件。

<a href="" id="link-states"></a>链接状态  
NDIS 端口链接状态为类似于链接的状态的微型端口适配器与相关联的和中指定[ **NDIS\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)结构。 端口链接状态指示媒体链接连接的状态和链接速度。 一个端口的链接状态可以是不同于关联的微型端口适配器的链接状态。

<a href="" id="authentication-states"></a>身份验证状态  
NDIS 端口身份验证状态指示是否控制端口 （需要授权），数据传输的方向 (发送、 接收和 / 或)，和端口 （获得授权，或未授权） 的授权状态。 如果不受控制的端口，则忽略的已经过身份验证和未经过身份验证状态。

微型端口驱动程序可以激活一个端口或停用的端口与即插即用事件。 有关激活和停用端口的详细信息，请参阅[激活 NDIS 端口](activating-an-ndis-port.md)并[Deactivating NDIS 端口](deactivating-an-ndis-port.md)。

过量驱动程序使用[OID\_代\_端口\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)要获取在指定的端口的当前状态的 OID **PortNumber** 成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构。 NDIS 处理此 OID 和微型端口驱动程序不会收到此 OID 查询。

支持 NDIS 端口的微型端口驱动程序必须使用[ **NDIS\_状态\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)状态指示，指示在 NDIS 端口的状态更改。 微型端口驱动程序必须在中设置的端口号**PortNumber**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构。

使用 NDIS 和基础驱动程序[OID\_代\_端口\_身份验证\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-authentication-parameters)OID 以设置 NDIS 端口的当前身份验证状态。 支持 NDIS 端口的微型端口驱动程序必须支持此 OID。

 

 





