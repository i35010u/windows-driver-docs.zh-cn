---
title: Hyper-V 可扩展交换机 OID 请求
description: Hyper-V 可扩展交换机 OID 请求
ms.assetid: 0B6D1628-DD83-4EA6-B5D5-33D74AD45EFD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4e07c06b0bc9c666ea54829c8fd8135d1ecf03e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211055"
---
# <a name="hyper-v-extensible-switch-oid-requests"></a>Hyper-V 可扩展交换机 OID 请求


Hyper-v 可扩展交换机接口包含按以下方式使用的对象标识符 (OID) 请求：

-   由可扩展交换机扩展颁发的 OID 请求，用于查询可扩展交换机的当前配置。 例如，筛选器驱动程序 (也称为 *hyper-v 可扩展交换机扩展*) 可以发出 [oid \_ 交换机 \_ NIC \_ 数组](./oid-switch-nic-array.md) 的 oid 查询请求，以获取一个数组。 数组中的每个元素指定与可扩展交换机端口关联的网络适配器的配置参数。

    有关详细信息，请参阅 [查询 Hyper-v 可扩展交换机配置](querying-the-hyper-v-extensible-switch-configuration.md)。

-   可扩展交换机接口发出的 OID 请求，通知基础扩展有关可扩展交换机配置的更改。 例如，可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ 端口 \_ CREATE](./oid-switch-port-create.md) 的 oid 集请求，通知有关创建可扩展交换机端口的扩展。

    有关详细信息，请参阅 [接收 OID 有关 Hyper-v 可扩展交换机配置更改的请求](receiving-oid-requests-about-hyper-v-extensible-switch-configuration-changes.md)。

-   从可扩展交换机接口转发到可扩展交换机控制路径扩展的 Hyper-v 子分区请求。 这允许扩展获取有关分区中使用的网络接口的配置信息。

    例如，扩展性接口中可扩展交换机的协议边缘转发 Oid 的 OID 集请求 [ \_ 802 \_ 3 \_ \_ \_ ](./oid-802-3-add-multicast-address.md) 从子分区向下扩展了可扩展的交换机控制路径。 这允许扩展插件获取此分区中的网络接口使用的多播地址配置。

    有关详细信息，请参阅 [从 Hyper-v 子分区转发 OID 请求](forwarding-oid-requests-from-a-hyper-v-child-partition.md)。

有关扩展和 NDIS 筛选器驱动程序如何处理 OID 请求的详细信息，请参阅 [筛选器模块 OID 请求](filter-module-oid-requests.md)。

 

