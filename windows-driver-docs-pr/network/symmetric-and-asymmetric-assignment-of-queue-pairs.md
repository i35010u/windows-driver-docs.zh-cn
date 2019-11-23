---
title: 队列对的对称和非对称分配
description: 队列对的对称和非对称分配
ms.assetid: B4BA1567-D536-4E7D-924C-7476FB82DAEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b10f4a40f3dd5038630f859f39c8b4038a2c5480
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841789"
---
# <a name="symmetric-and-asymmetric-assignment-of-queue-pairs"></a>队列对的对称和非对称分配


队列对由网络适配器上的单独传输队列和接收队列组成。 创建 VPort 时，将在虚拟端口（VPort）上配置队列对。 与默认 VPort 关联的队列对是在创建交换机时通过 oid 的 OID 方法[\_请求\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)来配置的。 一个或多个队列对在非默认 VPort 上，通过 oid\_NIC 的 oid 方法请求[\_交换机\_CREATE\_VPort](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)。

每个非默认 VPort 可以配置为具有不同的队列对数。 这称为队列对的*非对称分配*。 如果微型端口驱动程序不支持非对称分配，则每个非默认 VPort 将配置为具有相同数量的队列对。 这称为队列对的*对称分配*。

微型端口驱动程序使用[**NDIS\_NIC\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构在[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)期间公布其 VPort 和队列对功能。 该驱动程序通过将 NDIS\_NIC\_交换机\_\_CAP 设置为在此结构的**NicSwitchCapabilities**成员中\_非默认\_支持的标志，来公布其对队列对的非对称分配的支持。\_\_\_\_

如果微型端口驱动程序支持非对称队列对分配，则虚拟化堆栈会将每个非默认 VPort 配置为具有不同的队列对数。 如果微型端口驱动程序支持对称队列对分配，则虚拟化堆栈会将每个 VPort 配置为具有相同数量的队列对。

**请注意**  在非默认的 VPorts 上支持对称或非对称队列对分配的微型端口驱动程序必须支持在默认 VPort 上分配不同数目的队列对。 默认 VPort 始终连接到网络适配器的 PF。

 

队列对配置是在默认的 VPort 创建时指定的，或通过 oid [\_NIC\_交换机\_CREATE\_VPort](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport) and [oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)\_\_\_\_ 配置参数在[**NDIS\_NIC\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构（与两个 OID 请求关联）中指定。

例如，假定微型端口驱动程序通过将[**NDIS\_nic 的以下成员\_开关\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构，在 nic 交换机上公布 VPorts 和 queue 对的配置：

-   **MaxNumQueuePairs**设置为128。

-   **MaxNumVPorts**设置为64。

-   **MaxNumQueuePairsPerNonDefaultPort**设置为4。

如果微型端口驱动程序不支持非默认 VPorts 上队列对的非对称配置，则在创建 VPorts 时，虚拟化堆栈可以指定以下队列对配置：

-   63非默认的 VF VPorts 每个队列对，其中每个都包含一个队列对，默认 PF 为 VPort。
-   31个非默认的 VF VPorts 每个队列对，其中每个都有一个队列对，默认 PF 为 VPort。

**请注意**  从 Windows Server 2012 开始，仅支持一个默认的 VPort 并且始终连接到网络适配器的 PF。

 

 

 





