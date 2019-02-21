---
title: HYPER-V 可扩展交换机 OID 请求
description: HYPER-V 可扩展交换机 OID 请求
ms.assetid: 0B6D1628-DD83-4EA6-B5D5-33D74AD45EFD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 447a4aaf2898c9f089067f3d43c8b4b20eaf1529
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541614"
---
# <a name="hyper-v-extensible-switch-oid-requests"></a>HYPER-V 可扩展交换机 OID 请求


HYPER-V 可扩展交换机接口包括以下方面使用的对象标识符 (OID) 请求：

-   要查询的可扩展交换机的当前配置的可扩展交换机扩展由颁发的 OID 请求。 例如，筛选器驱动程序 (也称为*HYPER-V 可扩展交换机扩展*) 可以发出的 OID 查询请求[OID\_切换\_NIC\_数组](https://msdn.microsoft.com/library/windows/hardware/hh598261)到获取一个数组。 数组中的每个元素指定与可扩展交换机端口相关联的网络适配器的配置参数。

    有关详细信息，请参阅[查询的 HYPER-V 可扩展交换机配置](querying-the-hyper-v-extensible-switch-configuration.md)。

-   OID 请求由可扩展交换机接口以通知有关可扩展交换机配置更改的基础扩展。 例如，可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_端口\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598272)以通知有关的可扩展交换机端口创建的扩展。

    有关详细信息，请参阅[有关的 HYPER-V 可扩展交换机配置更改接收 OID 请求](receiving-oid-requests-about-hyper-v-extensible-switch-configuration-changes.md)。

-   通过可扩展交换机控制路径转发由可扩展交换机接口扩展的 OID 请求从 HYPER-V 子分区。 这允许扩展来获取分区中使用的网络接口的配置信息。

    例如，扩展性接口中的可扩展交换机的协议边缘将转发的 OID 集请求[OID\_802\_3\_添加\_多播\_地址](https://msdn.microsoft.com/library/windows/hardware/ff569068)从可扩展交换机控制路径下的子分区。 这允许扩展来获取由该分区中的网络接口的多播的地址配置。

    有关详细信息，请参阅[转发来自 HYPER-V 子分区的 OID 请求](forwarding-oid-requests-from-a-hyper-v-child-partition.md)。

有关如何扩展和 NDIS 筛选器驱动程序的详细信息处理 OID 请求，请参阅[筛选器模块 OID 请求](filter-module-oid-requests.md)。

 

 





