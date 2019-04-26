---
title: 即插即用的处理和协议驱动程序中的电源管理事件
description: 处理协议驱动程序中的 PnP 事件和电源管理事件
ms.assetid: 97cc51f1-7d83-4bf1-87e3-7d986f54e7a1
keywords:
- 协议驱动程序 WDK 网络、 电源管理
- NDIS 协议驱动程序 WDK、 电源管理
- 协议驱动程序 WDK 网络插
- NDIS 协议驱动程序 WDK，插
- 电源管理 WDK NDIS 协议
- 即插即用 WDK NDIS 协议
- 通知 WDK 即插即用，协议的 NDIS 驱动程序
- 事件通知 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4c28205f9594fe4939d32173b54fb9261d2b5d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325720"
---
# <a name="handling-pnp-events-and-power-management-events-in-a-protocol-driver"></a>处理协议驱动程序中的 PnP 事件和电源管理事件

当操作系统对表示网络接口卡 (NIC) 的目标设备对象发出插即用 (PnP) I/O 请求数据包 (IRP) 或电源管理 IRP 时，NDIS 截获 IRP。 NDIS 指示通过调用驱动程序的每个绑定的协议驱动程序和每个绑定的中间驱动程序的事件[ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263)函数。 在调用*ProtocolNetPnPEvent*，NDIS 将传递一个指向[ **NET\_PNP\_事件\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff568752) ，其中包含NET\_PNP\_事件结构。 NET\_PNP\_事件结构描述的即插即用事件或指示的电源管理事件。 有关协议驱动程序即插即用接口的详细信息，请参阅[协议驱动程序中处理即插即用事件通知](handling-pnp-event-notifications-in-a-protocol-driver.md)。

以下列表包含 PnP 和电源管理事件，如所示**NetEvent** NET 中的代码\_PNP\_事件结构：

-   **NetEventSetPower**

    指示设置 Power 请求，它指定微型端口适配器应转换为特定电源状态。 电源管理 – 注意协议驱动程序应始终成功此事件，通过返回 NDIS\_状态\_成功。 旧的协议驱动程序可以返回 NDIS\_状态\_不\_以指示 NDIS 应取消其绑定从微型端口适配器的支持。

    发出 set power 请求后, NDIS 暂停驱动程序堆栈，如果微型端口适配器正在过渡到低功耗状态。 NDIS 微型端口适配器转换到工作状态 (D0)，则将重新启动之前设置电源请求驱动程序堆栈。 有关暂停和重新启动驱动程序堆栈的详细信息，请参阅[暂停驱动程序堆栈](pausing-a-driver-stack.md)。

    如果微型端口适配器在低功耗状态，协议驱动程序不能发出任何 OID 请求。 此要求是添加到驱动程序堆栈处于已暂停状态时应用的其他限制的其他的电源管理限制。

    如果基础的微型端口适配器是电源管理感知，微型端口驱动程序设置**布尔**的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)到**NULL**和 NDIS 集**布尔**隶属[**NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)到**NULL**。

    **请注意**从 NDIS 6.30 开始后通知此事件，必须停止生成新的 I/O 请求协议驱动程序，应等待的任何挂起的 I/O 请求调用的上下文中完成[ *ProtocolNetPnPEvent*](https://msdn.microsoft.com/library/windows/hardware/ff570263)。

    有关设置电源事件的详细信息，请参阅[处理即插即用事件和中间驱动程序中的电源管理事件](handling-pnp-events-and-power-management-events-in-an-intermediate-dri.md)。

-   **NetEventQueryPower**

    指示查询能力请求，哪些查询的基础的微型端口适配器可以建立到特定的电源状态的转换。 协议驱动程序应始终成功**NetEventQueryPower** 。 建立活动连接后，协议驱动程序可以调用[ **PoRegisterSystemState** ](https://msdn.microsoft.com/library/windows/hardware/ff559731)注册连续的忙碌状态。 只要状态注册生效时，电源管理器不会尝试将系统进入睡眠状态。 协议驱动程序的连接成为非活动状态后，通过调用取消状态注册[ **PoUnregisterSystemState**](https://msdn.microsoft.com/library/windows/hardware/ff559794)。 协议驱动程序应永远不会尝试防止系统转换到的睡眠状态的故障**NetEventQueryRemoveDevice**。 请注意， **NetEventQueryPower**始终跟**NetEventSetPower**。 一个**NetEventSetPower** ，设置设备的当前电源状态实际上会取消**NetEventQueryPower**。

    **请注意**通知此事件的 NDIS 6.30 从开始协议驱动程序应等待完成的任何挂起的 I/O 请求调用的上下文中[ *ProtocolNetPnPEvent*](https://msdn.microsoft.com/library/windows/hardware/ff570263).

-   **NetEventQueryRemoveDevice**

    指示查询删除设备请求，哪些查询是否可以无需中断操作删除 NIC。 如果协议驱动程序不能释放某一设备 （例如，因为设备正在使用中），它必须失败**NetEventQueryRemoveDevice**通过返回 NDIS\_状态\_失败。

-   **NetEventCancelRemoveDevice**

    指示取消删除设备请求，这将取消删除基础 nic。 协议驱动程序应始终成功此事件，通过返回 NDIS\_状态\_成功。

-   **NetEventReconfigure**

    指示的配置已更改的网络组件。 例如，如果用户更改了 tcp/ip 的 IP 地址，NDIS 指示此事件来使用 TCP/IP 协议**NetEventReconfigure**代码。 协议驱动程序可以在极少数情况下，返回了失败代码如果不能应用所指示的配置更改，并且没有任何可用的默认值。 尝试分配内存失败是协议在其中返回了失败代码将用例的示例。 返回错误代码可能会导致系统提示用户重新启动系统。

    应验证协议**NetEventReconfigure**的相关的数据传递给其[ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263)函数。 有关此类数据的详细信息，请参阅[ **NET\_PNP\_协议驱动程序的事件**](https://msdn.microsoft.com/library/windows/hardware/ff568751)。

-   **NetEventBindList**

    指示协议驱动程序已重新配置其绑定列表处理顺序。 此列表指示相对顺序处理，例如，可能被路由到多个绑定之一的用户请求时要应用于协议的绑定。 与此事件传递的缓冲区包含格式为以 NULL 结尾的 Unicode 字符串的设备名称的列表。 每个设备名称的格式等同于*DeviceName*传递给调用的参数[ *ProtocolBindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570220)。

    应验证协议**NetEventBindList**的相关的数据传递给其*ProtocolNetPnPEvent*函数。 有关此类数据的详细信息，请参阅[ **NET\_PNP\_协议驱动程序的事件**](https://msdn.microsoft.com/library/windows/hardware/ff568751)。

    应验证协议**NetEventBindList**的相关的数据传递给其*ProtocolNetPnPEvent*函数。 有关此类数据的详细信息，请参阅[ **NET\_PNP\_协议驱动程序的事件**](https://msdn.microsoft.com/library/windows/hardware/ff568751)。

-   **NetEventBindsComplete**

    指示协议驱动程序已绑定到可以绑定到的所有 Nic。 NDIS 除非即插即用的 NIC 插入到系统中，将不会指示任何绑定到协议驱动程序的更多信息。

-   **NetEventPnPCapabilities**

    指示用户已启用或禁用基础适配器的唤醒功能。 ( *ProtocolBindingContext* NDIS 将传递给参数*ProtocolNetPnPEvent*指定的绑定。)

-   **NetEventPause**

    指示指定的协议绑定，应输入 thePausing 状态。 NDIS 完成所有未完成发送请求的绑定后，绑定将进入暂停状态。 有关暂停绑定的详细信息，请参阅[暂停绑定](pausing-a-binding.md)。

-   **NetEventRestart**

    指示指定的协议绑定已进入正在重新启动状态。 协议驱动程序已准备好继续发送和接收操作的绑定后，该绑定将进入运行状态。 有关重新启动绑定的详细信息，请参阅[重新启动绑定](restarting-a-binding.md)。

-   **NetEventPortActivation**

    指示激活与指定绑定相关联的端口的列表。 有关暂停绑定的详细信息，请参阅[处理端口激活即插即用事件](handling-the-port-activation-pnp-event.md)。

-   **NetEventPortDeactivation**

    表示与指定绑定相关联的端口的列表的停用操作。 有关暂停绑定的详细信息，请参阅[处理端口停用的即插即用事件](handling-the-port-deactivation-pnp-event.md)。

-   **NetEventIMReEnableDevice**

    指示为 NDIS 6.0 或更高版本的中间驱动程序的虚拟微型端口已更改配置。 **NetEventIMReEnableDevice**类似于**NetEventReconfigure**事件只不过中间驱动程序将收到此事件的单个虚拟微型端口和**NetEventReconfigure**事件适用于所有中间驱动程序的虚拟微型端口。 例如，中间驱动程序收到**NetEventIMReEnableDevice**事件时用户禁用然后再启用设备管理器或另一个源从单个虚拟微型端口。 中间驱动程序电源管理的示例，请参阅[NDIS MUX 中间驱动程序和通知对象](https://go.microsoft.com/fwlink/p/?LinkId=617916)中提供的驱动程序示例[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

**缓冲区**NET 成员\_PNP\_事件结构指向包含特定于所指示的事件的信息的缓冲区。

协议驱动程序可以完成对调用*ProtocolNetPnPEvent*使用以异步方式[ **NdisCompleteNetPnPEvent**](https://msdn.microsoft.com/library/windows/hardware/ff561705)。