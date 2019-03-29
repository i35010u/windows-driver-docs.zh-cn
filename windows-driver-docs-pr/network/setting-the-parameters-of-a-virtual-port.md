---
title: 设置虚拟端口的参数
description: 设置虚拟端口的参数
ms.assetid: 92CBE5B2-897D-4B34-9AB9-8207C42A72BF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 322132216739466da54c1fb790f9d5ee208373dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575248"
---
# <a name="setting-the-parameters-of-a-virtual-port"></a>设置虚拟端口的参数


基础驱动程序可以在 NIC 上支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器的交换机上更改虚拟端口 (VPort) 的参数。 设置对象标识符 (OID) 的驱动程序问题的请求[OID\_NIC\_交换机\_VPORT\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451825)要更改这些参数。

基础驱动程序将发出此 OID 集请求之前，必须将格式化[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构使用参数，VPort 上进行更改。 然后，该驱动程序初始化[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构的 OID 请求和集**InformationBuffer**成员添加到指向**NDIS\_NIC\_交换机\_VPORT\_参数**结构。

可以更改仅有限 VPort 的配置参数。 基础驱动程序指定要更改设置的以下成员的参数[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构：

-   **SwitchId**成员必须设置为 NIC 开关的参数为要返回的标识符。

    **请注意**  从 Windows Server 2012 开始，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 交换机*。 **SwitchId**成员必须设置为 NDIS\_默认\_交换机\_id。

     

-   **VPortId**成员必须设置为与 VPort 关联的标识符。 基础驱动程序将获取通过以下方式之一的 VPort 标识符：

    -   从上一个 OID 方法请求的[OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)。

    -   从上一个 OID 方法请求的[OID\_NIC\_交换机\_枚举\_VPORTS](https://msdn.microsoft.com/library/windows/hardware/hh451821)。

-   合适的 NDIS\_NIC\_交换机\_VPORT\_PARAMS\_*Xxx*\_CHANGED 标志必须设置**标志**成员。 成员[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构只能如果相应 NDIS 更改\_NIC\_交换机\_VPORT\_PARAMS\_*Xxx*\_中 Ntddndis.h 定义已更改的标志。

-   成员[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构，它们分别对应于 NDIS\_NIC\_交换机\_VPORT\_PARAMS\_*Xxx*\_设置已更改标志**标志**成员，请使用 VPort 配置设置要更改的参数。

从 Windows Server 2012，只有以下的成员开始[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构可以是通过 OID 集请求的更改[OID\_NIC\_交换机\_VPORT\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451825):

<a href="" id="portname"></a>**PortName**  
此成员包含 VPort 的用户友好说明。

<a href="" id="interruptmoderation"></a>**InterruptModeration**  
此成员指定 VPort 的中断裁决设置。

<a href="" id="processoraffinity"></a>**ProcessorAffinity**  
此成员指定的组编号和此 VPort 可以与之关联的 Cpu 的位图。

基础驱动程序必须遵循以下准则，以便更改**ProcessorAffinity** VPort 的成员：

-   此成员是仅对附加到 PF.VPorts 有效 此字段不是有效的非默认附加到 VF VPorts。

-   对于非默认 VPorts 附加到 PF，VPort 创建时，必须指定至少一个处理器。 VPort 创建后，可以更改与非默认 VPort 关联的处理器关联。

    **请注意**  通过 OID 方法请求的创建非默认 VPorts [OID\_NIC\_开关\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)。

     

<a href="" id="vportstate"></a>**VPortState**  
此成员指定 VPort 的当前状态。

基础驱动程序必须遵循以下准则，以便更改**VPortState** VPort 的成员：

-   对于非默认附加到 VF VPort **VPortState**成员必须始终设置为**NdisNicSwitchVPortStateActivated**。

-   对于非默认附加到 pf，PF VPort **VPortState**成员必须设置为**NdisNicSwitchVPortStateDeactivated** VPort 创建时。 OID 设置的请求后，仅激活 PF VPort [OID\_NIC\_交换机\_VPORT\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451825)基础驱动程序中，若要向激活更改 VPortState 颁发状态。

    非默认 VPort 激活时，PF 微型端口驱动程序可以为 VPort，如通过分配的共享内存分配的资源[ **NdisAllocateSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff561616)。 PF 微型端口驱动程序可能会为分配的资源 VPort 直到该驱动程序中删除通过 OID 集请求的 VPort 激活后，随时[OID\_NIC\_交换机\_删除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818).

-   默认 VPort 为始终处于激活状态。 值**VPortState**成员必须始终设置为**NdisNicSwitchVPortStateActivated**默认 VPort。

-   当 VPort 处于激活状态时，它不能停用。 PF 微型端口驱动程序可以接收和传输来自 VPort 数据包，仅当它处于激活状态和 VPort 上设置相应的 MAC 筛选器。 但是，VPort 删除通过 OID 集请求的后[OID\_NIC\_交换机\_删除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)，驱动程序必须释放 VPort 为已分配的资源。 该驱动程序还必须取消所有挂起的传输或接收的数据包 VPort 上的操作。

后 PF 微型端口驱动程序收到的 OID 集请求[OID\_NIC\_交换机\_VPORT\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451825)，驱动程序使用的配置参数配置硬件. 该驱动程序只能更改这些配置参数标识的 NDIS\_NIC\_交换机\_VPORT\_参数\_*Xxx*\_已更改在标记**标志**的成员[ **NDIS\_NIC\_开关\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构。

 

 





