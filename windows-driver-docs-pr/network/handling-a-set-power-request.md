---
title: 处理设置电源请求
description: 处理设置电源请求
ms.assetid: c69d4a9b-009a-4320-8e20-32a9cf9113bf
keywords:
- 设置 power 请求 WDK NDIS 中间
- 睡眠状态 WDK NDIS 中间
- WDK NDIS 中间的工作状态
- 备用标志 WDK NDIS 中间
- 电源状态 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 209a5eade46e226cf29319332410ff92fd4b7f9e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379828"
---
# <a name="handling-a-set-power-request"></a>处理设置电源请求





中间的驱动程序必须处理请求，以将幂设置到工作状态 （网络设备电源状态的 D0） 和休眠状态 （网络设备电源状态 D1、 D2 或 D3 的）。 电源状态变量和一个备用标志，还应该维护中间驱动程序。 讨论了这些问题，本主题中。

中间驱动程序电源管理的示例，请参阅[NDIS MUX 中间驱动程序和通知对象](https://go.microsoft.com/fwlink/p/?LinkId=617916)中的驱动程序示例[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

### <a name="handling-a-set-power-request-to-a-sleeping-state"></a>处理 Set Power 请求为睡眠状态

有两种情况下，中间驱动程序必须处理 set power 请求为睡眠状态：

-   NDIS 中间驱动程序的虚拟微型端口上边缘进入睡眠状态的请求。

-   当它收到插即用 (PnP) 事件通知时，中间驱动程序协议下边缘处理基础的微型端口驱动程序转换为休眠状态。

这些事件可以按任意顺序和一个事件不会不一定是附带有其他。

当虚拟微型端口上边缘的中间驱动程序收到将幂设置为休眠状态的请求时，用于处理请求的事件序列如下所示：

1.  NDIS 调用[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)函数的每个协议驱动程序绑定到虚拟微型端口。 在调用*ProtocolNetPnPEvent*指定**NetEventSetPower**睡眠状态的事件。 绑定到中间驱动程序的协议驱动程序停止发送网络数据和中间驱动程序对虚拟微型端口进行 OID 请求。 协议下边缘中间的驱动程序可以继续向下发送网络数据和请求，直到 NDIS 指示基础微型端口驱动程序正在转换到休眠状态。

2.  NDIS 发出后暂停基础驱动程序，然后选择虚拟微型端口**NetEventSetPower**事件。 用于暂停指定的原因是转换到低功耗状态。 有关暂停虚拟微型端口的详细信息，请参阅[暂停适配器](pausing-an-adapter.md)。

    **请注意**  否 OID 请求可以发送到虚拟微型端口，而在低功耗状态下，是除[OID\_PNP\_设置\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)。

     

3.  NDIS 问题[OID\_PNP\_设置\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)中间驱动程序的虚拟微型端口的请求。 中间驱动程序接受该请求通过返回 NDIS\_状态\_成功。 中间驱动程序必须不会传播 OID\_PNP\_设置\_POWER 请求为基础的微型端口驱动程序。 中间驱动程序完成此请求后，它不应指示任何更接收到的网络数据或指示状态，即使它会从基础微型端口驱动程序，接收网络数据和状态指示。

当中间驱动程序的协议下边缘转换为休眠状态基础的微型端口驱动程序时，用于处理转换的事件序列如下所示：

1.  NDIS 调用[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)中间驱动程序协议下边缘的函数。 在调用*ProtocolNetPnPEvent*指定**NetEventSetPower**睡眠状态的事件。 中间驱动程序必须停止发送网络数据和向基础微型端口驱动程序发出 OID 请求。 如果有未完成的请求或发送，则中间驱动程序应返回 NDIS\_状态\_调用 PENDING *ProtocolNetPnPEvent*。 中间的驱动程序调用[ **NdisCompleteNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscompletenetpnpevent)若要完成对调用*ProtocolNetPnPEvent*。 中间的驱动程序的协议边缘仍然可以从基础的微型端口驱动程序获取收到的数据包和状态指示。 可以忽略接收的网络数据。 如果中间驱动程序的实现依赖于监视基础微型端口驱动程序的状态，应仍会监视状态指示。

2.  NDIS 暂停中间驱动程序的协议边缘，并发出后暂停 underying 微型端口适配器**NetEventSetPower**事件。 用于暂停指定的原因是转换到低功耗状态。 有关暂停的协议绑定的详细信息，请参阅[暂停绑定](pausing-a-binding.md)。

    **请注意**  否 OID 请求可以发送到基础的微型端口适配器，而在低功耗状态下，是除[OID\_PNP\_设置\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)。

     

3.  NDIS 问题[OID\_PNP\_设置\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)基础微型端口驱动程序的请求。 但是，如果基础微型端口驱动程序不支持电源管理，将停止它。 在这种情况下，即使 NDIS 就会停止基础微型端口驱动程序，它不会请求要从基础的微型端口驱动程序和 NIC 取消绑定的中间驱动程序协议 基础的微型端口驱动程序已成功完成处理 OID （或暂停微型端口驱动程序） 后，它将不会指示任何更多网络数据或状态。

### <a name="handling-a-set-power-request-to-the-working-state"></a>处理 Set Power 请求到工作状态

有两种情况下，中间驱动程序将处理 set power 请求到工作状态：

-   NDIS 中间驱动程序的虚拟微型端口上边缘转到工作状态的请求。

-   中间驱动程序协议下边缘处理基础的微型端口驱动程序转换到工作状态，当它收到插即用 (PnP) 事件通知。

一个事件不会不一定是附带有其他并且按任意顺序可能会发生这些事件。

当虚拟微型端口上边缘的中间驱动程序收到的请求将幂设置为工作状态时，用于处理请求的事件序列如下所示：

1.  NDIS 问题[OID\_PNP\_设置\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)到中间驱动程序的虚拟微型端口。 中间驱动程序将返回 NDIS\_状态\_集 power 请求成功。 中间驱动程序必须不会传播 OID\_PNP\_设置\_POWER 请求为基础的微型端口驱动程序。

2.  NDIS 重启虚拟微型端口，并发出集 power OID 后会重新启动基础驱动程序。 有关重新启动虚拟微型端口信息的详细信息，请参阅[启动适配器](starting-an-adapter.md)。

3.  NDIS 调用[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)基础协议驱动程序的函数。 在调用*ProtocolNetPnPEvent*指定**NetEventSetPower**设置工作状态 (D0) 事件。 绑定的协议驱动程序可以开始将网络数据发送到中间驱动程序的虚拟微型端口。

当中间驱动程序的协议下边缘转换到工作状态基础的微型端口驱动程序时，用于处理转换的事件序列如下所示：

1.  NDIS 问题[OID\_PNP\_设置\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)基础的微型端口驱动程序或调用其[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)如果基础微型端口驱动程序已停止处理程序。

2.  NDIS 发出 OID 后重新启动基础微型端口驱动程序，然后中间 NDIS 和基础的微型端口适配器的协议边缘。 有关暂停的协议绑定的详细信息，请参阅[重新启动绑定](restarting-a-binding.md)。

3.  NDIS 调用[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)中间驱动程序的函数。 在调用*ProtocolNetPnPEvent*指定**NetEventSetPower**设置工作状态 (D0) 事件。 中间驱动程序可以开始将网络数据发送到基础微型端口驱动程序。

### <a name="power-states-and-the-standby-flag"></a>电源状态和备用标志

中间的驱动程序应维护独立的电源状态变量的每个虚拟微型端口实例，每个基础微型端口驱动程序的驱动程序是绑定。 中间驱动程序还应该维护的 StandingBy 标志的是每个虚拟微型端口：

-   设置为 **，则返回 TRUE**虚拟微型端口或基础微型端口驱动程序的电源状态当离开 D0。

-   设置为**FALSE** D0 返回虚拟微型端口或基础微型端口驱动程序的电源状态。

**请注意**  MUX 中间驱动程序，可以有多个与基础的微型端口驱动程序相关联的虚拟微型端口或多个基础的微型端口与每个虚拟微型端口相关联。 当任何微型端口适配器的电源状态更改时，所有关联的微型端口的行为也会受到影响。 如何影响行为是特定于实现的。 例如，实现负载平衡故障转移 (LBFO) 解决方案的驱动程序可能会停用虚拟微型端口，单个基础的微型端口驱动程序被停用时。 但是，取决于基础的微型端口驱动程序的驱动程序实现任何基础的微型端口驱动程序被停用时，将需要停用的虚拟微型端口。

 

按如下所示处理请求时，中间驱动程序应使用 StandingBy 标志和电源状态变量：

-   在驱动程序[ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)函数应失败，除非虚拟微型端口和其基础的微型端口适配器都在 D0。

-   在驱动程序[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数应始终成功 OID\_PNP\_查询\_电源以确保该驱动程序接收后续的 OID\_PNP\_设置\_电源请求。

-   在驱动程序[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数，如果虚拟微型端口不在 D0 或者 StandingBy 是应失败**TRUE**。 否则，它应队列单个请求，如果基础微型端口驱动程序不在 D0。 当基础的微型端口驱动程序状态将变为 D0 时，应处理的排队的请求。

-   只有基础微型端口驱动程序和虚拟微型端口都 D0 中间驱动程序的虚拟微型端口应报告状态。

 

 





