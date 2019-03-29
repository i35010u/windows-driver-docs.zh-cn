---
title: 初始化中间驱动程序
description: 初始化中间驱动程序
ms.assetid: cd4903f8-f522-403a-bec4-03ee7e82dcac
keywords:
- NDIS 中间层驱动程序 WDK，初始化
- 驱动程序 WDK 的中间连接网络、 初始化
- 初始化中间驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f39bdea54c77f822487f6d77c6ceeccb44ed345
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564288"
---
# <a name="initializing-an-intermediate-driver"></a>初始化中间驱动程序



NDIS 中间层驱动程序注册其*MiniportXxx*函数并将其*ProtocolXxx*函数的上下文中其[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程。 若要注册其*MiniportXxx*函数，请调用中间驱动程序必须[NdisMRegisterMiniportDriver](https://msdn.microsoft.com/library/windows/hardware/ff563654)函数与的 NDIS\_中间\_驱动程序标志设置。 该标记位于[ **NDIS\_微型端口\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565958)驱动程序通过在结构*MiniportDriverCharacteristics*。 若要注册其*ProtocolXxx*函数，请调用中间驱动程序必须[NdisRegisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff564520)函数。

[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)返回 STATUS_SUCCESS 或其等效的 NDIS_STATUS_SUCCESS，如果该驱动程序已成功注册为 NDIS 中间驱动程序。 如果 DriverEntry 失败并初始化传播由返回的错误状态**NdisXxx**函数或通过内核模式下支持例程，该驱动程序将不继续加载。 **DriverEntry**必须执行同步; 即，它不能返回 STATUS_PENDING 或其等效 NDIS_STATUS_PENDING。

中间驱动程序注册到 NDIS [DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程至少必须：

- 调用[NdisMRegisterMiniportDriver](https://msdn.microsoft.com/library/windows/hardware/ff563654) NDIS_INTERMEDIATE_DRIVER 标志设置要注册的驱动程序的函数*MiniportXxx*函数。
- 调用[NdisRegisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff564520)函数来注册的驱动程序*ProtocolXxx*函数如果驱动程序随后将本身绑定到基础的 NDIS 驱动程序。
- 调用[NdisIMAssociateMiniport](https://msdn.microsoft.com/library/windows/hardware/ff562717)函数来通知 NDIS 驱动程序的微型端口上边缘与协议下边缘之间的关联。

如果在出现错误**DriverEntry**后**NdisMRegisterMiniportDriver**驱动程序必须调用成功，返回[NdisMDeregisterMiniportDriver](https://msdn.microsoft.com/library/windows/hardware/ff563578)函数之前**DriverEntry**返回。 如果**DriverEntry**成功，驱动程序必须调用**NdisMDeregisterMiniportDriver**从其[MiniportDriverUnload](https://msdn.microsoft.com/library/windows/hardware/ff559378)函数。

中间驱动程序共享的大部分**DriverEntry**协议驱动程序和微型端口驱动程序的要求。

初始化中间驱动程序的虚拟微型端口驱动程序调用时发生[NdisIMInitializeDeviceInstanceEx](https://msdn.microsoft.com/library/windows/hardware/ff562727)函数从其[ProtocolBindAdapterEx](https://msdn.microsoft.com/library/windows/hardware/ff570220)函数。

NDIS 调用*ProtocolBindAdapterEx*毕竟基础微型端口驱动程序函数已初始化。

实际上， **DriverEntry** NDIS 中间驱动程序函数可以忽略*RegistryPath*指针后将其传递给**NdisMRegisterMiniportDriver**。 此类驱动程序，也可忽略*DriverObject*后将其传递给指针**NdisMRegisterMiniportDriver**。 但是，该驱动程序应保存微型端口驱动程序返回的句柄值**NdisMRegisterMiniportDriver**处*NdisMiniportDriverHandle* 返回将协议句柄值**NdisRegisterProtocolDriver**处*NdisProtocolHandle*以便后续调用**NdisXxx**函数。 在中间驱动程序*ProtocolBindAdapterEx*函数将驱动程序绑定到每个基础微型端口驱动程序之前其*MiniportInitializeEx*函数调用以初始化中间虚拟微型端口驱动程序。 主管更高级别协议驱动程序随后将绑定本身到它创建虚拟微型端口。 此策略使 NDIS 中间驱动程序将在绑定到基础的微型端口驱动程序的功能根据虚拟微型端口创建的资源分配。
