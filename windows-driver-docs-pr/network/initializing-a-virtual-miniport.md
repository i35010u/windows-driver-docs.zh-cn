---
title: 初始化虚拟微型端口
description: 初始化虚拟微型端口
ms.assetid: 5f2e23a9-375b-4b0d-95d2-5a3af1acb3be
keywords:
- 正在初始化虚拟微型端口
- virtual 微型端口 WDK 网络
- NDIS 中间驱动程序 WDK，virtual 微型端口
- 中间驱动程序 WDK 网络，虚拟微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c63bc08df4e433c1784da4b64cca0d5fa5be3c83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824495"
---
# <a name="initializing-a-virtual-miniport"></a>初始化虚拟微型端口





若要启动虚拟小型端口的初始化，中间驱动程序将调用[**NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)函数。 中间驱动程序通常从其[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数进行此调用。 在中间驱动程序调用**NdisIMInitializeDeviceInstanceEx** ，并使用插即用器请求 NDIS 启动虚拟设备后，ndis 将调用驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数。

如果即插即用 manager 在**NdisIMInitializeDeviceInstanceEx**返回之前启动虚拟设备，则对*MiniportInitializeEx*的调用可以在**NdisIMInitializeDeviceInstanceEx**的上下文中。 如果中间驱动程序提供了多个虚拟小型端口，则驱动程序必须为其提供的每个虚拟小型端口调用**NdisIMInitializeDeviceInstanceEx** 。

在*MiniportInitParameters*中，ndis 会将初始化参数传递到[**ndis\_微型\_INIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)结构中的*MiniportInitializeEx* 。 结构的**IMDeviceInstanceContext**成员指定指向虚拟设备的上下文区域的指针。 驱动程序在*DeviceContext*参数将此指针传递到[**NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)函数。

在*MiniportInitializeEx*中，中间驱动程序执行初始化虚拟小型端口所需的操作。 此初始化与任何其他微型端口适配器的初始化类似。

 

 





