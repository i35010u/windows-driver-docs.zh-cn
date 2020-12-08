---
title: 初始化中间驱动程序
description: 初始化中间驱动程序
keywords:
- NDIS 中间驱动程序 WDK，初始化
- 中间驱动程序 WDK 网络，初始化
- 初始化中间驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e407a4de05ffcfea9a0f8599bf919445ab350b14
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803691"
---
# <a name="initializing-an-intermediate-driver"></a>初始化中间驱动程序



NDIS 中间驱动程序在其 [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程的上下文中注册其 *MiniportXxx* 函数及其 *ProtocolXxx* 函数。 若要注册其 *MiniportXxx* 函数，中间驱动程序必须调用 [NdisMRegisterMiniportDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) 函数并设置 NDIS \_ 中间 \_ 驱动程序标志。 此标志位于驱动程序通过 *MiniportDriverCharacteristics* 传递的 [**NDIS \_ 微型端口 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构中。 若要注册其 *ProtocolXxx* 函数，中间驱动程序必须调用 [NdisRegisterProtocolDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver) 函数。

如果成功注册为 NDIS 中间驱动程序的驱动程序， [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)将返回 STATUS_SUCCESS 或其等效 NDIS_STATUS_SUCCESS。 如果 DriverEntry 通过传播 **NdisXxx** 函数返回的错误状态或内核模式支持例程来初始化失败，则不会保持加载该驱动程序。 **DriverEntry** 必须同步执行;也就是说，它不能返回 STATUS_PENDING 或其等效 NDIS_STATUS_PENDING。

若要将中间驱动程序注册到 NDIS， [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程至少必须：

- 调用 [NdisMRegisterMiniportDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) 函数，并将 NDIS_INTERMEDIATE_DRIVER 标志设置为注册驱动程序的 *MiniportXxx* 函数。
- 调用 [NdisRegisterProtocolDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver) 函数以注册驱动程序的 *ProtocolXxx* 函数（如果驱动程序随后将自身绑定到基础 NDIS 驱动程序）。
- 调用 [NdisIMAssociateMiniport](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimassociateminiport) 函数以通知 NDIS 有关驱动程序的小型端口上边缘与协议下边缘之间的关联的信息。

如果在 **NdisMRegisterMiniportDriver** 成功返回后 **DriverEntry** 中出现错误，则驱动程序必须在 **DriverEntry** 返回前调用 [NdisMDeregisterMiniportDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver)函数。 如果 **DriverEntry** 成功，则驱动程序必须从其 [MiniportDriverUnload](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload)函数调用 **NdisMDeregisterMiniportDriver** 。

中级驱动程序共享了协议驱动程序和微型端口驱动程序的大部分 **DriverEntry** 要求。

当驱动程序从其[ProtocolBindAdapterEx](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数调用[NdisIMInitializeDeviceInstanceEx](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)函数时，将会初始化中间驱动程序的虚拟小型端口。

在所有基础微型端口驱动程序都初始化之后，NDIS 将调用 *ProtocolBindAdapterEx* 函数。

实际上，NDIS 中间驱动程序的 **DriverEntry** 函数可以在将 *RegistryPath* 指针传递到 **NdisMRegisterMiniportDriver** 后将其忽略。 此类驱动程序还可以在将 *DriverObject* 指针传递到 **NdisMRegisterMiniportDriver** 之后将其忽略。 但是，驱动程序应将 **NdisMRegisterMiniportDriver** 处的 "微型端口驱动程序句柄" 值保存到 *NdisMiniportDriverHandle* ，并将 **NdisRegisterProtocolDriver** 处返回的协议句柄值保存到 *NdisProtocolHandle* ，以便对 **NdisXxx** 函数进行后续调用。 中间驱动程序的 *ProtocolBindAdapterEx* 函数将驱动程序绑定到每个基础微型端口驱动程序，然后调用其 *MiniportInitializeEx* 函数以初始化中间驱动程序的虚拟小型端口。 同样，更高级别的协议驱动程序随后会将自己绑定到它创建的虚拟小型端口。 使用此策略，NDIS 中间驱动程序可以根据绑定到的基础微型端口驱动程序的功能，在创建虚拟小型端口时分配资源。
