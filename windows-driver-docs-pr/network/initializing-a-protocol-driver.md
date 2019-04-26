---
title: 初始化协议驱动程序
description: 初始化协议驱动程序
ms.assetid: 1479d59b-7c8b-495b-86c7-72f1b7e334e4
keywords:
- 协议驱动程序 WDK 连接网络、 初始化
- NDIS 协议驱动程序 WDK，初始化
- 初始化协议驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d043809b5a93e4e6feb8a08dce74b6f8c3fdf3e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324993"
---
# <a name="initializing-a-protocol-driver"></a>初始化协议驱动程序




系统调用协议驱动程序[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程后它会加载该驱动程序。 协议驱动程序加载为系统服务。 它们可以加载在任何时间之前、 期间或之后的微型端口驱动程序加载。

协议驱动程序分配驱动程序资源和注册*ProtocolXxx*中的函数**DriverEntry**。 这包括的 CoNDIS 客户端和独立调用管理器。 若要注册其*ProtocolXxx* NDIS 函数，协议驱动程序调用[NdisRegisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff564520)函数。

[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)返回 STATUS_SUCCESS 或其等效的 NDIS_STATUS_SUCCESS，如果该驱动程序已成功注册为 NDIS 协议驱动程序。 如果**DriverEntry**传播由返回的错误状态将失败并初始化**NdisXxx**函数或通过内核模式下支持例程，该驱动程序将不继续加载。 **DriverEntry**必须执行同步; 即，它不能返回 STATUS_PENDING 或其等效 NDIS_STATUS_PENDING。

[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113) NDIS 协议驱动程序函数必须调用[NdisRegisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff564520)函数。 若要注册的驱动程序*ProtocolXxx* NDIS 库使用的入口点，协议驱动程序初始化[ **NDIS_PROTOCOL_DRIVER_CHARACTERISTICS** ](https://msdn.microsoft.com/library/windows/hardware/ff566825)结构和将其传递给**NdisRegisterProtocolDriver**。

调用 NdisRegisterProtocolDriver 的驱动程序必须做好对任何其 ProtocolXxx 函数的直接调用。

协议的 NDIS 驱动程序提供以下*ProtocolXxx*函数，它们是旧驱动程序提供的函数的更新的版本：

[*ProtocolSetOptions*](https://msdn.microsoft.com/library/windows/hardware/ff570269)

[*ProtocolBindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570220)

[*ProtocolUnbindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570278)

[*ProtocolOpenAdapterCompleteEx*](https://msdn.microsoft.com/library/windows/hardware/ff570265)

[*ProtocolCloseAdapterCompleteEx*](https://msdn.microsoft.com/library/windows/hardware/ff570236)

[*ProtocolNetPnPEvent*](https://msdn.microsoft.com/library/windows/hardware/ff570263)

[*ProtocolUninstall*](https://msdn.microsoft.com/library/windows/hardware/ff570279)

协议的 NDIS 驱动程序提供以下*ProtocolXxx*函数发送和接收操作：

[**ProtocolReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff570267)

[**ProtocolSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff570268)

所有类型的协议的 NDIS 驱动程序应都注册完备[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)并[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)函数来支持插即用 (PnP)。 一般情况下， [DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)函数应调用[NdisRegisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff564520)立即之前它将返回 STATUS_SUCCESS 或 NDIS_STATUS_SUCCESS 将 status 值的控件。

将导出的一组标准的内核模式驱动程序例程，除了其 NDIS 定义任何协议驱动程序*ProtocolXxx*函数必须传递到给定的驱动程序对象中设置这些驱动程序例程的入口点其[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)函数。 有关功能的这样的协议驱动程序的详细信息**DriverEntry**函数中，请参阅[编写 DriverEntry 例程](../kernel/writing-a-driverentry-routine.md)。

如果尝试将驱动程序执行网络 I/O 操作失败，所需的资源分配[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)应释放所有资源已分配之前它将返回具有的状态不是 STATUS_ 控件成功或 NDIS_STATUS_SUCCESS。

如果在成功调用后出现错误[NdisRegisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff564520)，该驱动程序必须调用[NdisDeregisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff561743)函数之前**DriverEntry**返回。

若要允许协议驱动程序以配置可选服务，NDIS 调用*ProtocolSetOptions*协议驱动程序的调用的上下文中的函数**NdisRegisterProtocolDriver**。 可选的服务的详细信息，请参阅[配置可选协议驱动程序服务](configuring-optional-protocol-driver-services.md)。

CoNDIS 客户端驱动程序必须调用[NdisSetOptionalHandlers](https://msdn.microsoft.com/library/windows/hardware/ff564550)函数从[ *ProtocolSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff570269)函数。 该驱动程序初始化[ **NDIS_CO_CLIENT_OPTIONAL_HANDLERS** ](https://msdn.microsoft.com/library/windows/hardware/ff564884)结构，并将其在传递*OptionalHandlers*参数**NdisSetOptionalHandlers**。

此外必须调用独立调用管理器的 CoNDIS [NdisSetOptionalHandlers](https://msdn.microsoft.com/library/windows/hardware/ff564550)函数从[ *ProtocolSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff570269)函数。 该驱动程序初始化[ **NDIS_CO_CALL_MANAGER_OPTIONAL_HANDLERS** ](https://msdn.microsoft.com/library/windows/hardware/ff564883)结构，并将其在传递*OptionalHandlers*参数**NdisSetOptionalHandlers**。

MCMs 不是协议驱动程序。 因此，它们必须调用[NdisSetOptionalHandlers](https://msdn.microsoft.com/library/windows/hardware/ff564550)函数从[MiniportSetOptions](https://msdn.microsoft.com/library/windows/hardware/ff559443)函数。 初始化 MCM [ **NDIS_CO_CALL_MANAGER_OPTIONAL_HANDLERS** ](https://msdn.microsoft.com/library/windows/hardware/ff564883)结构，并将其在传递*OptionalHandlers*参数**NdisSetOptionalHandlers**。

NDIS 中注销，协议驱动程序调用[NdisDeregisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff561743)从其[卸载](https://msdn.microsoft.com/library/windows/hardware/ff564886)例程。

若要卸载协议驱动程序之前，请执行清理操作，协议驱动程序可以注册[ *ProtocolUninstall* ](https://msdn.microsoft.com/library/windows/hardware/ff570279)函数。 *ProtocolUninstall*函数是可选的。 例如，可能需要中间驱动程序的协议下边缘*ProtocolUninstall*函数。 中间驱动程序可以释放在其协议边缘资源*ProtocolUninstall* NDIS 调用前其[ *MiniportDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff559378)函数。

 

 





