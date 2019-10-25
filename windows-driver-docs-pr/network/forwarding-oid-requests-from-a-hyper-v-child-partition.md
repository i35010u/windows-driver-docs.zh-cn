---
title: 从 Hyper-V 子分区转发 OID 请求
description: 从 Hyper-V 子分区转发 OID 请求
ms.assetid: 35EA9964-4CD0-4636-9573-65F37393B7E2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e093a82a2e661526b204bcb55d2866a2bcd59f4c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841751"
---
# <a name="forwarding-oid-requests-from-a-hyper-v-child-partition"></a>从 Hyper-V 子分区转发 OID 请求


多路广播对象标识符（OID）请求，包括[OID\_802\_3\_添加\_多播\_地址](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-add-multicast-address)和[OID\_802\_3\_删除\_多播\_地址](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-delete-multicast-address)由过量协议和筛选器驱动程序（在以下各项中运行）发出：

-   在 Hyper-v 父分区中运行的管理操作系统。

-   在 Hyper-v 子分区中运行 Windows Vista 或更高版本的 Windows 操作系统的来宾操作系统。

可扩展交换机接口将这些 OID 请求沿可扩展交换机控制路径向下转发。 这允许扩展获取有关分区中使用的网络接口的配置信息。

例如，可扩展交换机的协议边缘将 Oid 的 OID 集请求转发[\_802\_3\_从子分区向下添加\_多播\_地址](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-add-multicast-address)。 这允许扩展插件获取此分区中的网络接口使用的多播地址配置。

当这些多播 OID 请求到达可扩展交换机接口时，可扩展交换机的协议边缘将在[**NDIS\_交换机\_NIC\_oid\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构中封装 OID 请求。 协议边缘还会按以下方式设置此结构的成员：

-   **SourcePortId**和**SourceNicIndex**成员设置为从中发出 OID 请求的分区所使用的端口和网络适配器的相应值。

    **注意**  如果多播 OID 请求源自管理操作系统，则协议边缘会将这些成员设置为可扩展交换机内部网络适配器的值。

     

-   **DestinationPortId**和**DestinationNicIndex**成员设置为零。 这指定封装的 OID 请求将传递到控件路径中的扩展。

-   **OidRequest**成员设置为封装的 oid 请求[ **\_请求结构的 NDIS\_OID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)的地址。

然后，协议边缘发出[OID\_交换机\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)请求，以将封装的 OID 请求向下转发到可扩展的交换机控制路径。 基础转发扩展可以检查这些封装的 OID 请求并保留它们指定的多播地址信息。 例如，如果扩展会将多播数据包转发到可扩展交换机端口，则可能需要此信息。

有关可扩展交换机控制路径的详细信息，请参阅[Hyper-v 可扩展交换机控制路径](hyper-v-extensible-switch-control-path.md)。

 

 





