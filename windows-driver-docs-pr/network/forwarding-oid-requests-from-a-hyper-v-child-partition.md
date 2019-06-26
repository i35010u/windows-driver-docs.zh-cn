---
title: 从 Hyper-V 子分区转发 OID 请求
description: 从 Hyper-V 子分区转发 OID 请求
ms.assetid: 35EA9964-4CD0-4636-9573-65F37393B7E2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 044ba4d6dbf61df881eab0d0acf64316d2f9895d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382782"
---
# <a name="forwarding-oid-requests-from-a-hyper-v-child-partition"></a>从 Hyper-V 子分区转发 OID 请求


多播的对象标识符 (OID) 请求，包括[OID\_802\_3\_添加\_多播\_地址](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-add-multicast-address)并[OID\_802\_3\_删除\_多播\_地址](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-delete-multicast-address)、 颁发的过量协议和筛选器驱动程序运行所示：

-   管理操作系统的 HYPER-V 父分区中运行。

-   来宾操作系统运行 Windows Vista 或更高版本的 Windows 操作系统的 HYPER-V 子分区中。

可扩展交换机接口将转发这些 OID 请求下可扩展交换机控制路径。 这允许扩展来获取分区中使用的网络接口的配置信息。

例如，可扩展交换机的协议边缘将转发的 OID 集请求[OID\_802\_3\_添加\_多播\_地址](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-add-multicast-address)从子分区向下可扩展交换机控制路径。 这允许扩展来获取由该分区中的网络接口的多播的地址配置。

当这些多播的 OID 请求在可扩展交换机接口，可扩展交换机的协议边缘封装 OID 请求内的[ **NDIS\_切换\_NIC\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构。 协议边缘还按以下方式设置此结构的成员：

-   **SourcePortId**并**SourceNicIndex**成员设置为 OID 请求产生的分区所使用的端口和网络适配器的相应值。

    **请注意**  可扩展交换机内部网络适配器，协议边缘如果多播的 OID 请求来自管理操作系统，将这些成员设置为值。

     

-   **DestinationPortId**并**DestinationNicIndex**成员设置为零。 这指定封装的 OID 请求是要传递到中的控制路径的扩展。

-   **OidRequest**成员设置为的地址[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)封装 OID 请求的结构。

然后发出协议边缘[OID\_切换\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)下可扩展交换机控制路径将封装的 OID 请求转发的请求。 基础转发扩展可以检查这些封装的 OID 请求并保留他们指定的多播的地址信息。 例如，该扩展可能需要此信息，如果它源自其转发到可扩展交换机端口的多路广播的数据包。

有关可扩展交换机控制路径的详细信息，请参阅[HYPER-V 可扩展交换机控制路径](hyper-v-extensible-switch-control-path.md)。

 

 





