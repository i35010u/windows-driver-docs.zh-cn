---
title: 注册为 NDIS 中间驱动程序
description: 注册为 NDIS 中间驱动程序
ms.assetid: 4a095fa7-0d8f-4d7d-885c-bc43cd34c784
keywords:
- 注册中间驱动程序
- 驱动程序 WDK 的中间连接网络、 注册
- NDIS 中间层驱动程序 WDK，注册
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 170d1baa08dfde890655d6fa1343da2878338dc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542544"
---
# <a name="registering-as-an-ndis-intermediate-driver"></a>注册为 NDIS 中间驱动程序





NDIS 中间驱动程序必须注册其*MiniportXxx*函数并将其*ProtocolXxx* NDIS 函数的上下文中其[ **DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113)函数。 若要注册其*MiniportXxx*函数，请调用中间驱动程序必须[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)与的 NDIS\_中间\_设置驱动程序标志。 该标记位于[ **NDIS\_微型端口\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565958)驱动程序通过在结构*MiniportDriverCharacteristics* 。 此调用将中间驱动程序的导出*MiniportXxx*函数。 有关注册的详细信息*MiniportXxx*函数，请参阅[微型端口驱动程序作为注册中间驱动程序](registering-an-intermediate-driver-as-a-miniport-driver.md)。

请注意，中间驱动程序控制当其虚拟微型端口进行了初始化，，因此，当驱动程序已准备好接受发送并请求在适配器上。 NDIS 调用中间驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)插即用 (PnP) 管理器已开始虚拟微型端口设备以及之后的中间驱动程序已调用函数[**NdisIMInitializeDeviceInstanceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff562727)为该设备。 在调用*MiniportInitializeEx*在更高版本时可能发生，因此不一定是对的调用的上下文中**NdisIMInitializeDeviceInstanceEx**。 如果中间驱动程序导出多个虚拟微型端口驱动程序必须调用**NdisIMInitializeDeviceInstanceEx**用于使可用于网络请求每个虚拟微型端口。

若要注册其*ProtocolXxx*函数，请调用中间驱动程序必须[ **NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520)函数。 有关注册的详细信息*ProtocolXxx*函数，请参阅[作为协议驱动程序注册中间驱动程序](registering-an-intermediate-driver-as-a-protocol.md)。

 

 





