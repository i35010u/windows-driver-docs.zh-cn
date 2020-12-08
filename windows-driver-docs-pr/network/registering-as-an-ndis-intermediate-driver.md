---
title: 注册为 NDIS 中间驱动程序
description: 注册为 NDIS 中间驱动程序
keywords:
- 注册中间驱动程序
- 中间驱动程序 WDK 网络，注册
- NDIS 中间驱动程序 WDK，注册
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c2b7fa7e2ac9b85df25617d25d9d9ba112aa8c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812829"
---
# <a name="registering-as-an-ndis-intermediate-driver"></a>注册为 NDIS 中间驱动程序





NDIS 中间驱动程序必须在其 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数的上下文中使用 ndis 注册其 *MiniportXxx* 函数及其 *ProtocolXxx* 函数。 若要注册其 *MiniportXxx* 函数，中间驱动程序必须调用 [**NDISMREGISTERMINIPORTDRIVER**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) 并 \_ 设置 NDIS 中间 \_ 驱动程序标志。 此标志位于驱动程序通过 *MiniportDriverCharacteristics* 传递的 [**NDIS \_ 微型端口 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构中。 此调用导出中间驱动程序的 *MiniportXxx* 函数。 有关注册 *MiniportXxx* 函数的详细信息，请参阅 [将中间驱动程序注册为微型端口驱动程序](registering-an-intermediate-driver-as-a-miniport-driver.md)。

请注意，中间驱动程序会控制初始化其虚拟微型端口的时间，从而在驱动程序准备好接受适配器上的发送和请求时进行控制。 即插即用 (PnP) 管理器启动了虚拟微型端口设备后，并且在中间驱动程序为该设备调用 [**NdisIMInitializeDeviceInstanceEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)之后，NDIS 将调用中间驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数。 对 *MiniportInitializeEx* 的调用可能会在稍后发生，因此不一定会出现在对 **NdisIMInitializeDeviceInstanceEx** 的调用的上下文中。 如果中间驱动程序导出多个虚拟小型端口，则驱动程序必须为每个虚拟小型端口调用 **NdisIMInitializeDeviceInstanceEx** ，以便为网络请求提供此功能。

若要注册其 *ProtocolXxx* 函数，中间驱动程序必须调用 [**NdisRegisterProtocolDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver) 函数。 有关注册 *ProtocolXxx* 函数的详细信息，请参阅 [将中间驱动程序注册为协议驱动程序](registering-an-intermediate-driver-as-a-protocol.md)。

 

