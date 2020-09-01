---
title: 查询虚拟端口的参数
description: 查询虚拟端口的参数
ms.assetid: 482DA041-2C70-438A-8D29-0F338CDCF935
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6bd8329a3e39b55c97e473373a9e885558db651
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215106"
---
# <a name="querying-the-parameters-of-a-virtual-port"></a>查询虚拟端口的参数


过量驱动程序可以在支持单一根 i/o 虚拟化 (SR-IOV) 的网络适配器上的 NIC 交换机上，获取虚拟端口 (VPort) 的参数。 驱动程序) [oid \_ NIC \_ SWITCH \_ VPORT \_ 参数](./oid-nic-switch-vport-parameters.md) 的方法请求 (oid 发出对象标识符，以获取这些参数。

在过量驱动程序发出此 OID 方法请求之前，它必须初始化 [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) 结构。 驱动程序必须按以下方式设置此结构的成员：

-   **SwitchId**成员必须设置为要为其返回参数的 NIC 交换机的标识符。

    **注意**   从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 " *默认 NIC 交换机*"。 **SwitchId**成员必须设置为 NDIS \_ 默认 \_ 交换机 \_ ID。

     

-   **VPortId**成员必须设置为与 VPort 关联的标识符。 过量驱动程序通过以下方式之一获取 VPort 标识符：

    -   从 Oid NIC 交换机的上一个 OID 方法请求 [ \_ \_ \_ 创建 \_ VPORT](./oid-nic-switch-create-vport.md)。

    -   从 [oid \_ NIC \_ 交换机 \_ 枚举 \_ VPORTS](./oid-nic-switch-enum-vports.md)的上一个 oid 方法请求开始。

成功从此 OID 方法请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的指针。 此结构包含指定 VPort 的参数。

NDIS 为微型端口驱动程序处理 [OID \_ NIC \_ 交换机 \_ VPORT \_ 参数](./oid-nic-switch-vport-parameters.md) 请求。 NDIS 从检查以下源中返回的数据的内部缓存返回信息：

-   [Oid \_ NIC \_ 交换器 \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md)的 oid 方法请求。

-   OID 设置 [oid \_ NIC \_ SWITCH \_ VPORT \_ 参数](./oid-nic-switch-vport-parameters.md)的请求。

 

