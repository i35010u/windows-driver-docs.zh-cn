---
title: 处理协议驱动程序中的 PnP 和电源管理事件
description: 处理协议驱动程序中的 PnP 事件和电源管理事件
keywords:
- 协议驱动程序 WDK 网络，电源管理
- NDIS 协议驱动程序 WDK，电源管理
- 协议驱动程序 WDK 网络，即插即用
- NDIS 协议驱动程序 WDK，即插即用
- 电源管理 WDK NDIS 协议
- 即插即用 WDK NDIS 协议
- 通知 WDK PnP，NDIS 协议驱动程序
- 事件通知 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 666a8fec893708df54e9f374e64631c9a4eade68
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837213"
---
# <a name="handling-pnp-events-and-power-management-events-in-a-protocol-driver"></a>处理协议驱动程序中的 PnP 事件和电源管理事件

当即插即用操作系统 (PnP) i/o 请求数据包 (IRP) 或电源管理 IRP 发送到表示网络接口卡 (NIC) 的目标设备对象时，NDIS 会截获 IRP。 NDIS 通过调用驱动程序的 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event) 函数，指示每个绑定协议驱动程序的事件和每个绑定的中间驱动程序。 在对 *ProtocolNetPnPEvent* 的调用中，NDIS 传递指向包含 net pnp 事件结构的 [**net \_ pnp \_ 事件 \_ 通知**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification) 的指针 \_ \_ 。 NET \_ PNP \_ 事件结构描述了所指示的 PNP 事件或电源管理事件。 有关协议驱动程序 PnP 接口的详细信息，请参阅 [在协议驱动程序中处理 PnP 事件通知](handling-pnp-event-notifications-in-a-protocol-driver.md)。

以下列表包含 PnP 和电源管理事件，如 NET **NetEvent** \_ PnP 事件结构中的 NetEvent 代码所示 \_ ：

-   **NetEventSetPower**

    指示设置的电源请求，该请求指定微型端口适配器应转换为特定电源状态。 支持电源管理的协议驱动程序应始终通过返回 NDIS 状态成功来成功完成此事件 \_ \_ 。 旧协议驱动程序可以返回 \_ \_ 不 \_ 受支持的 ndis 状态，以指示 ndis 应从微型端口适配器将其解除绑定。

    发出设置电源请求后，如果微型端口适配器正在转换为低功耗状态，NDIS 将暂停驱动程序堆栈。 如果微型端口适配器正在转换到工作状态 (D0) ，NDIS 将在设置电源请求之前重新启动驱动程序堆栈。 有关暂停和重新启动驱动程序堆栈的详细信息，请参阅 [暂停驱动程序堆栈](pausing-a-driver-stack.md)。

    如果微型端口适配器处于低功耗状态，则协议驱动程序无法发出任何 OID 请求。 此要求是额外的电源管理限制，添加到了驱动程序堆栈处于暂停状态时所应用的其他限制。

    如果基础微型端口适配器不是电源管理-感知，微型端口驱动程序会将 [**ndis \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的 **PowerManagementCapabilities** 成员设置为 **Null** ，ndis 会将 [**ndis \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)的 **PowerManagementCapabilities** 成员设置为 **null**。

    **注意**  从 NDIS 6.30 开始，在收到此事件的通知后，协议驱动程序必须停止生成新的 i/o 请求，且不应在调用 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)的上下文中等待完成任何挂起的 i/o 请求。

    有关设置电源事件的详细信息，请参阅 [在中间驱动程序中处理 PnP 事件和电源管理事件](handling-pnp-events-and-power-management-events-in-an-intermediate-dri.md)。

-   **NetEventQueryPower**

    指示查询电源请求，该请求查询基础微型端口适配器是否可以转换为特定电源状态。 协议驱动程序应始终成功 **NetEventQueryPower** 。 建立活动连接后，协议驱动程序可以调用 [**PoRegisterSystemState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregistersystemstate) 来注册连续繁忙状态。 只要状态注册生效，电源管理器不会尝试将系统置于睡眠状态。 在连接处于非活动状态后，协议驱动程序会通过调用 [**PoUnregisterSystemState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pounregistersystemstate)取消状态注册。 协议驱动程序绝不应尝试防止系统通过 **NetEventQueryRemoveDevice** 故障转换为休眠状态。 请注意， **NetEventQueryPower** 总是后跟 **NetEventSetPower**。 设置设备当前电源状态的 **NetEventSetPower** 取消了 **NetEventQueryPower**。

    **注意**  从 NDIS 6.30 开始，在收到此事件的通知后，在对 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)的调用上下文中，协议驱动程序不应等待完成任何挂起的 i/o 请求。

-   **NetEventQueryRemoveDevice**

    指示查询删除设备请求，该请求查询是否可以在不中断操作的情况下删除 NIC。 例如，如果某个协议驱动程序无法释放设备 (例如，因为设备正在使用) ，则它必须通过返回 NDIS 状态失败来 **NetEventQueryRemoveDevice** 故障 \_ \_ 。

-   **NetEventCancelRemoveDevice**

    指示取消删除设备请求，该请求取消了基础 NIC 的删除。 协议驱动程序应始终通过返回 NDIS 状态成功来成功完成此事件 \_ \_ 。

-   **NetEventReconfigure**

    指示网络组件的配置已更改。 例如，如果用户更改了 TCP/IP 的 IP 地址，NDIS 会使用 **NetEventReconfigure** 代码来指示 tcp/ip 协议的此事件。 如果协议驱动程序无法应用指定的配置更改并且没有可用的默认值，则在极少数情况下，它可能会返回失败代码。 尝试分配内存失败是一个示例，其中，协议返回故障代码。 返回错误代码可能会导致提示用户重新启动系统。

    协议应验证传递到其 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)函数的 **NetEventReconfigure** 相关数据。 有关此类数据的详细信息，请参阅 [**\_ \_ 适用于协议驱动程序的 NET PNP 事件**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)。

-   **NetEventBindList**

    向协议驱动程序指示已重新配置其绑定列表处理顺序。 此列表指示要在处理时应用到协议的绑定的相对顺序，例如，可能会路由到多个绑定之一的用户请求。 随此事件传递的缓冲区包含格式为以 NULL 结尾的 Unicode 字符串格式的设备名称列表。 每个设备名称的格式与传递给对 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)的调用的 *DeviceName* 参数相同。

    协议应验证传递到其 *ProtocolNetPnPEvent* 函数的 **NetEventBindList** 相关数据。 有关此类数据的详细信息，请参阅 [**\_ \_ 适用于协议驱动程序的 NET PNP 事件**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)。

    协议应验证传递到其 *ProtocolNetPnPEvent* 函数的 **NetEventBindList** 相关数据。 有关此类数据的详细信息，请参阅 [**\_ \_ 适用于协议驱动程序的 NET PNP 事件**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)。

-   **NetEventBindsComplete**

    指示协议驱动程序已绑定到它可以绑定到的所有 Nic。 除非将 PnP NIC 插入系统，否则 NDIS 不会指示任何其他绑定到协议驱动程序。

-   **NetEventPnPCapabilities**

    指示用户启用或禁用了基础适配器的唤醒功能。  (NDIS 传递到 *ProtocolNetPnPEvent* 的 *ProtocolBindingContext* 参数指定绑定。 ) 

-   **NetEventPause**

    指示指定的协议绑定应进入 thePausing 状态。 当 NDIS 完成绑定的所有未完成的发送请求后，绑定将进入暂停状态。 有关暂停绑定的详细信息，请参阅 [暂停绑定](pausing-a-binding.md)。

-   **NetEventRestart**

    指示指定的协议绑定已进入重新启动状态。 在协议驱动程序准备好为绑定恢复发送和接收操作后，绑定将进入 "正在运行" 状态。 有关重新启动绑定的详细信息，请参阅 [重新启动绑定](restarting-a-binding.md)。

-   **NetEventPortActivation**

    指示激活与指定绑定关联的端口列表。 有关暂停绑定的详细信息，请参阅 [处理端口激活 PnP 事件](handling-the-port-activation-pnp-event.md)。

-   **NetEventPortDeactivation**

    指示停用与指定绑定关联的端口列表。 有关暂停绑定的详细信息，请参阅 [处理端口停用 PnP 事件](handling-the-port-deactivation-pnp-event.md)。

-   **NetEventIMReEnableDevice**

    指示对于 NDIS 6.0 或更高版本中间驱动程序的虚拟小型端口，配置已更改。 **NetEventIMReEnableDevice** 类似于 **NetEventReconfigure** 事件，只不过中间驱动程序接收单个虚拟小型端口的此事件， **NetEventReconfigure** 事件适用于所有中间驱动程序的虚拟微型端口。 例如，当用户禁用并启用设备管理器或其他源中的单个虚拟小型端口时，中间驱动程序将接收 **NetEventIMReEnableDevice** 事件。 有关中间驱动程序电源管理的示例，请参阅 GitHub 上的[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中提供的[NDIS MUX 中间驱动程序和通知对象](https://go.microsoft.com/fwlink/p/?LinkId=617916)驱动程序示例。

NET **Buffer** \_ PNP 事件结构的 buffer 成员 \_ 指向的缓冲区包含特定于所指示事件的信息。

协议驱动程序可以使用 [**NdisCompleteNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompletenetpnpevent)异步完成对 *ProtocolNetPnPEvent* 的调用。
