---
title: 队列对的对称和非对称分配
description: 队列对的对称和非对称分配
ms.assetid: B4BA1567-D536-4E7D-924C-7476FB82DAEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54cc1a7bc46684996c0b402af5665d536fb6e672
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362556"
---
# <a name="symmetric-and-asymmetric-assignment-of-queue-pairs"></a>队列对的对称和非对称分配


队列对由单独传输和接收的网络适配器上的队列。 当创建 VPort 虚拟端口 (VPort) 上配置队列对。 VPort 进行配置的时间通过 OID 方法请求的交换机创建的默认值与关联的队列对[OID\_NIC\_切换\_创建\_切换](https://msdn.microsoft.com/library/windows/hardware/hh451815)。 请求的一个或多个队列非默认配置对通过 OID 方法 VPort [OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)。

每个非默认 VPort 可以配置为具有不同数目的队列对。 这称为*非对称分配*队列对。 如果微型端口驱动程序不支持非对称分配，每个非默认 VPort 配置为有相同数目的队列对。 这称为*对称分配*队列对。

微型端口驱动程序会在其 VPort 和队列对功能通告[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)通过[ **NDIS\_NIC\_交换机\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)结构。 驱动程序播发的队列对非对称分配它支持通过设置 NDIS\_NIC\_交换机\_CAP\_非对称\_队列\_对\_为\_非默认\_VPORT\_中的受支持标志**NicSwitchCapabilities**此结构的成员。

如果微型端口驱动程序支持非对称队列对分配，虚拟化堆栈使用不同数量的队列对来配置每个非默认 VPort。 如果微型端口驱动程序支持对称队列对分配，虚拟化堆栈使用同一个队列对的数目来配置每个 VPort。

**请注意**  非默认 VPorts 支持任一对称或非对称队列对分配的微型端口驱动程序必须支持不同数目的队列对默认 VPort 上分配。 默认 VPort 始终附加到网络适配器的 PF.

 

队列对配置指定当创建或更新的 OID 请求通过非默认 VPort [OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)和[OID\_NIC\_交换机\_VPORT\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451825)。 中指定的配置参数[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构，它是两个相关联OID 的请求。

例如，假定微型端口驱动程序通过设置以下成员的播发 VPorts 和队列对 NIC 交换机上配置[ **NDIS\_NIC\_切换\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)结构：

-   **MaxNumQueuePairs**设置为 128。

-   **MaxNumVPorts**设置为 64。

-   **MaxNumQueuePairsPerNonDefaultPort**设置为 4。

如果微型端口驱动程序不支持非默认 VPorts 上的队列对非对称配置，虚拟化堆栈创建 VPorts 时可以指定以下队列对配置：

-   63 非默认 VF VPorts 与两个队列对每个队列对默认 PF VPort 以及。
-   31 非默认 VF VPorts 与四个队列对每个队列对默认 PF VPort 以及。

**请注意**  从 Windows Server 2012 开始，只有一个默认 VPort 支持，并且始终附加到网络适配器的 PF.

 

 

 





