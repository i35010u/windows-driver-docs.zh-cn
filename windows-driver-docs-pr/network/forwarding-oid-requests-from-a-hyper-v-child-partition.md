---
title: 从 Hyper-V 子分区转发 OID 请求
description: 从 Hyper-V 子分区转发 OID 请求
ms.assetid: 35EA9964-4CD0-4636-9573-65F37393B7E2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 451e9733db46b725d08077f6d24ccebf9410d80f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209743"
---
# <a name="forwarding-oid-requests-from-a-hyper-v-child-partition"></a>从 Hyper-V 子分区转发 OID 请求


多播对象标识符 (OID) 请求，包括 [oid \_ 802 \_ 3 \_ 添加 \_ 多播 \_ 地址](./oid-802-3-add-multicast-address.md) 和 [oid \_ 802 \_ 3 \_ 删除 \_ 多播 \_ 地址](./oid-802-3-delete-multicast-address.md)，由在以下各项中运行的过量协议和筛选器驱动程序发出：

-   在 Hyper-v 父分区中运行的管理操作系统。

-   在 Hyper-v 子分区中运行 Windows Vista 或更高版本的 Windows 操作系统的来宾操作系统。

可扩展交换机接口将这些 OID 请求沿可扩展交换机控制路径向下转发。 这允许扩展获取有关分区中使用的网络接口的配置信息。

例如，可扩展交换机的协议边缘转发 Oid 的 OID 集请求 802 3 在可扩展交换机控制路径的子分区中 [ \_ \_ \_ 添加 \_ 多播 \_ 地址](./oid-802-3-add-multicast-address.md) 。 这允许扩展插件获取此分区中的网络接口使用的多播地址配置。

当这些多播 OID 请求到达可扩展交换机接口时，可扩展交换机的协议边缘将在 [**NDIS \_ 交换机 \_ NIC \_ oid \_ 请求**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request) 结构内封装 OID 请求。 协议边缘还会按以下方式设置此结构的成员：

-   **SourcePortId**和**SourceNicIndex**成员设置为从中发出 OID 请求的分区所使用的端口和网络适配器的相应值。

    **注意**   如果多播 OID 请求源自管理操作系统，则协议边缘会将这些成员设置为可扩展交换机内部网络适配器的值。

     

-   **DestinationPortId**和**DestinationNicIndex**成员设置为零。 这指定封装的 OID 请求将传递到控件路径中的扩展。

-   **OidRequest**成员设置为封装的 oid 请求的[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的地址。

然后，协议边缘发出 [OID \_ 交换机 \_ NIC \_ 请求](./oid-switch-nic-request.md) 请求，以将封装的 OID 请求沿可扩展交换机控制路径向下转发。 基础转发扩展可以检查这些封装的 OID 请求并保留它们指定的多播地址信息。 例如，如果扩展会将多播数据包转发到可扩展交换机端口，则可能需要此信息。

有关可扩展交换机控制路径的详细信息，请参阅 [Hyper-v 可扩展交换机控制路径](hyper-v-extensible-switch-control-path.md)。

 

