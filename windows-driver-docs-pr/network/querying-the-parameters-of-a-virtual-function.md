---
title: 查询虚拟功能的参数
description: 查询虚拟功能的参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74c0e2a0c35dd00647a401f870675b09b2a8abf1
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248609"
---
# <a name="querying-the-parameters-of-a-virtual-function"></a>查询虚拟功能的参数


过量驱动程序或用户模式应用程序可以在支持单一根 i/o 虚拟化 (SR-IOV) 的网络适配器上，获取 PCI Express (PCIe) 虚)  (函数的当前参数。 驱动程序或应用程序发出对象标识符 (OID) 方法请求 [oid \_ NIC \_ SWITCH \_ VF \_ 参数](./oid-nic-switch-vf-parameters.md) 以获取这些参数。

在过量驱动程序发出此 OID 方法请求之前，它必须初始化 [**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters) 结构。 驱动程序或应用程序必须将 **VFId** 成员设置为要为其返回参数的 VF 的标识符。 可以通过以下方式获取 VF 标识符：

-   通过发出 [oid \_ NIC \_ 交换机 \_ 枚举 \_ VFS](./oid-nic-switch-enum-vfs.md)的 oid 方法请求。

    如果此 OID 请求成功完成，则过量驱动程序或用户模式应用程序将收到网络适配器上分配的所有 VFs 的列表。 列表中的每个元素都是一个 [**NDIS \_ NIC \_ 交换机 \_ vf \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info) 结构，其中包含由 **VFId** 成员指定的 VF 标识符。

-   通过发出 Oid NIC 交换机的 OID 方法请求 [ \_ \_ \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)。

    如果此 OID 请求成功完成，则过量驱动程序会在返回的 [**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构的 **VFID** 成员中接收新创建的 VF 的标识符。

    **注意**  只有过量驱动程序才能以这种方式获取 VF 标识符。

     

成功从 OID 方法请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构的指针。 此结构包含指定的 VF 的配置参数。

NDIS 为微型端口驱动程序处理 [OID \_ NIC \_ 交换机 \_ VF \_ 参数](./oid-nic-switch-vf-parameters.md) 请求。 NDIS 从检查以下源中返回的数据的内部缓存返回信息：

-   Oid NIC 交换机的 OID 方法请求 [ \_ \_ \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)。

-   Oid 设置 [oid \_ NIC \_ 开关 \_ VF \_ 参数](./oid-nic-switch-vf-parameters.md)的请求。

 

