---
title: 注册为 NDIS 中间驱动程序
description: 注册为 NDIS 中间驱动程序
ms.assetid: 4a095fa7-0d8f-4d7d-885c-bc43cd34c784
keywords:
- 注册中间驱动程序
- 中间驱动程序 WDK 网络，注册
- NDIS 中间驱动程序 WDK，注册
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a241f8ad4f596fa63b10936a6f86741503193f03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842082"
---
# <a name="registering-as-an-ndis-intermediate-driver"></a>注册为 NDIS 中间驱动程序





NDIS 中间驱动程序必须在其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数的上下文中使用 ndis 注册其*MiniportXxx*函数及其*ProtocolXxx*函数。 若要注册其*MiniportXxx*函数，中间驱动程序必须使用 NDIS\_中间\_驱动程序标志集来调用[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) 。 此标志位于[**NDIS\_微型端口\_驱动程序\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构，驱动程序在*MiniportDriverCharacteristics*上传递。 此调用导出中间驱动程序的*MiniportXxx*函数。 有关注册*MiniportXxx*函数的详细信息，请参阅[将中间驱动程序注册为微型端口驱动程序](registering-an-intermediate-driver-as-a-miniport-driver.md)。

请注意，中间驱动程序会控制初始化其虚拟微型端口的时间，从而在驱动程序准备好接受适配器上的发送和请求时进行控制。 即插即用（PnP）管理器启动了虚拟微型端口设备后，NDIS 调用了中间驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数，并在中间驱动程序为该设备调用[**NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)之后装置. 对*MiniportInitializeEx*的调用可能会在稍后发生，因此不一定会出现在对**NdisIMInitializeDeviceInstanceEx**的调用的上下文中。 如果中间驱动程序导出多个虚拟小型端口，则驱动程序必须为每个虚拟小型端口调用**NdisIMInitializeDeviceInstanceEx** ，以便为网络请求提供此功能。

若要注册其*ProtocolXxx*函数，中间驱动程序必须调用[**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)函数。 有关注册*ProtocolXxx*函数的详细信息，请参阅[将中间驱动程序注册为协议驱动程序](registering-an-intermediate-driver-as-a-protocol.md)。

 

 





