---
title: 指示连接状态
description: 指示连接状态
ms.assetid: 8a511c14-6b09-47fe-90de-6a90dab93171
keywords:
- WMI WDK 网络、 媒体连接状态
- 微型端口驱动程序 WDK 网络，媒体连接状态
- NDIS 微型端口驱动程序 WDK，媒体连接状态
- 连接状态 WDK 网络
- 媒体连接 WDK 网络
- NDIS_STATUS_MEDIA_CONNECT
- NDIS_STATUS_MEDIA_DISCONNECT
- WDK NDIS 微型端口的状态信息
- 状态指示 WDK 网络，媒体连接
- 睡眠状态 WDK 网络
- 唤醒状态 WDK 网络
- 重置状态 WDK 网络
- 正在停止状态 WDK 网络
- 正在初始化状态 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e20ba3d0a83831cf1482f79da792e21b10a3b921
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524688"
---
# <a name="indicating-connection-status"></a>指示连接状态





微型端口驱动程序调用[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)或[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)以指示媒体连接中的更改状态。 微型端口驱动程序将传递到以下状态指示之一**NdisM (Co) IndicateStatus**:

<a href="" id="ndis-status-media-connect"></a>NDIS\_状态\_媒体\_连接  
指示的媒体连接状态更改从已断开连接。 媒体连接状态时断开连接的适配器建立网络连接发生更改。 例如，适配器将连接时它进入范围 （适用于无线适配器） 或在用户连接的网络电缆。

<a href="" id="ndis-status-media-disconnect"></a>NDIS\_状态\_媒体\_断开连接  
表示媒体连接状态变化连接断开连接。 媒体断开连接状态的已连接的适配器失去网络连接时，将发生更改。 例如，适配器将失去连接，因为它不在范围内 （适用于无线适配器） 或用户断开网络电缆。

除非另行指定，微型端口驱动程序应检测的状态更改后的两秒内指示媒体连接状态更改。

微型端口驱动程序可以执行某些操作 （请参阅下面的列表） 时检查媒体连接状态。 如果状态是相同的操作完成后开始操作之前一样，微型端口驱动程序没有要报告操作过程中可能发生的任何状态更改。

以下列表描述，该值指示媒体连接状态更改的微型端口驱动程序的其他的要求：

<a href="" id="resetting"></a>重置  
NDIS 调用[ *MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432)重置微型端口驱动程序。 微型端口驱动程序可以同步或异步完成重置。

如果媒体连接状态重置后不同，该驱动程序应在完成重置后的两秒内指示状态。

微型端口驱动程序不应完成重置操作，直到它已确定媒体连接状态。

<a href="" id="halting"></a>正在停止  
微型端口驱动程序必须指示任何媒体连接状态更改时调用 NDIS [ *MiniportHaltEx*](https://msdn.microsoft.com/library/windows/hardware/ff559388)。

<a href="" id="initializing"></a>正在初始化  
NDIS 调用微型端口驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数以初始化适配器。 适配器在初始化期间，微型端口驱动程序必须遵循以下准则：

-   如果微型端口驱动程序返回从后未指示媒体连接状态*MiniportInitializeEx*，NDIS 使用的值**MediaConnectState**的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)结构，以确定媒体连接状态。 微型端口驱动程序与此结构提供 NDIS 驱动程序调用时[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)从其*MiniportInitializeEx*函数。

    **请注意**  如果**MediaConnectState**成员设置为 MediaConnectStateUnknown，NDIS 将继续像适配器已断开连接。

     

-   如果适配器连接后调用 NDIS *MiniportInitializeEx*，微型端口驱动程序可以指示 NDIS\_状态\_媒体\_连接在 5 秒后它将返回*MiniportInitializeEx*。

-   如果适配器已断开连接后调用 NDIS *MiniportInitializeEx*，微型端口驱动程序应指示 NDIS\_状态\_媒体\_在 2 秒后它将返回内的断开连接*MiniportInitializeEx*。

-   微型端口驱动程序应处理时初始化时， [OID\_常规\_媒体\_CONNECT\_状态](https://msdn.microsoft.com/library/windows/hardware/ff569604)或者[OID\_常规\_共同\_媒体\_CONNECT\_状态](https://msdn.microsoft.com/library/windows/hardware/ff569455)异步请求。 微型端口驱动程序不应完成之前此类请求后它已确定连接状态。

-   确定媒体连接状态不应延迟初始化。 如果有必要，微型端口驱动程序应启动进程来确定连接状态中的*MiniportInitializeEx*，并在以后完成过程。 例如，微型端口驱动程序可以设置一个计时器，以轮询的适配器的连接状态。

-   媒体断开连接在初始化期间，但不是应序列化的微型端口驱动程序，可以指示反序列化的微型端口驱动程序。

<a href="" id="sleeping"></a>睡眠状态  
微型端口驱动程序进入网络睡眠状态，当它收到[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)设置设备电源状态 D1、 D2 或 D3 的请求。

微型端口驱动程序时进入睡眠状态或处于睡眠状态时，必须指示任何媒体连接状态更改。

<a href="" id="waking"></a>唤醒  
微型端口驱动程序收到 OID 时从睡眠状态唤醒\_PNP\_设置\_POWER 请求设备电源状态设置为 D0。

如果适配器的媒体连接状态唤醒等同于状态后在处于休眠状态前，微型端口驱动程序不应指示媒体连接状态更改。 如果连接状态更改，微型端口驱动程序应唤醒后的两个几秒内指示新的连接状态。

时唤醒，微型端口驱动程序应处理 OID\_GEN\_媒体\_CONNECT\_状态或 OID\_常规\_共同\_媒体\_CONNECT\_状态以异步方式请求。 微型端口驱动程序不应完成之前此类请求后它已确定连接状态。

 

 





