---
title: 枚举网络适配器上的 NIC 交换机
description: 枚举网络适配器上的 NIC 交换机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5850532ec0afa47be4cbffd12546ef19e4b9b6de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823917"
---
# <a name="enumerating-nic-switches-on-a-network-adapter"></a>枚举网络适配器上的 NIC 交换机


覆盖驱动程序或用户应用程序可以获取在支持单个根 i/o 虚拟化 (SR-IOV) 的网络适配器上创建的所有 NIC 交换机的列表。 驱动程序或应用程序发出 (OID 的对象标识符) 用于获取此列表的 [oid \_ NIC \_ 交换机 \_ 枚举 \_ ](./oid-nic-switch-enum-switches.md) 的请求。

成功从此 OID 请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向缓冲区的指针，该缓冲区包含以下内容：

-   用于定义数组中的元素数的 [**NDIS \_ NIC \_ 交换机 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters) 结构。

-   [**NDIS \_ NIC \_ 交换机 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构的数组。 其中每个结构都包含有关在网络适配器上创建的单个 NIC 交换机的信息。

    **注意** 如果网络适配器没有 NIC 交换机，则驱动程序将 [**ndis \_ nic \_ 交换机 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)结构的 **NumElements** 成员设置为零，且不会返回任何 [**NDIS \_ nic \_ 交换机 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构。

     

**注意**  从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 *默认 NIC 交换机*，由 NDIS \_ 默认 \_ 交换机 \_ ID 标识符引用。

 

NDIS 处理适用于微型端口驱动程序的 [OID \_ NIC \_ 交换机 \_ 枚举 \_ 切换](./oid-nic-switch-enum-switches.md) 请求。 NDIS 从以下源中返回的数据的内部缓存返回信息：

-   注册表中的标准化 SR-IOV 关键字设置。 有关这些关键字的详细信息，请参阅 [sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

-   Oid [ \_ nic \_ 交换机 \_ 创建 \_ 交换机](./oid-nic-switch-create-switch.md) 和 [OID \_ nic \_ 交换机 \_ 参数](./oid-nic-switch-parameters.md)的 oid 请求。

**注意** NDIS 还在 [**ndis \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)和 [**ndis \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构中提供 **NicSwitchArray** 成员中的开关的枚举。 因此，过量协议和筛选器驱动程序不必发出 [OID \_ NIC \_ 交换机 \_ 枚举 \_ 开关](./oid-nic-switch-enum-switches.md) 请求来获取此信息。

 

 

