---
title: 指示连接状态
description: 指示连接状态
ms.assetid: 8a511c14-6b09-47fe-90de-6a90dab93171
keywords:
- WMI WDK 网络，媒体连接状态
- 微型端口驱动程序 WDK 网络，媒体连接状态
- NDIS 微型端口驱动程序 WDK，媒体连接状态
- 连接状态 WDK 网络
- 媒体连接 WDK 网络
- NDIS_STATUS_MEDIA_CONNECT
- NDIS_STATUS_MEDIA_DISCONNECT
- 状态信息 WDK NDIS 微型端口
- 状态指示 WDK 网络，媒体连接
- 睡眠状态 WDK 网络
- 唤醒状态 WDK 网络
- 正在重置状态 WDK 网络
- 停止状态 WDK 网络
- 正在初始化状态 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27f9759419fcae3deedde11c1138063d2946a4d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824705"
---
# <a name="indicating-connection-status"></a>指示连接状态





微型端口驱动程序调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)或[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)以指示媒体连接状态的更改。 微型端口驱动程序将以下状态指示之一传递给**NdisM （Co） IndicateStatus**：

<a href="" id="ndis-status-media-connect"></a>\_媒体\_连接的 NDIS\_状态  
指示媒体连接状态从 "已断开" 更改为 "已连接"。 如果断开连接的适配器建立网络连接，则会发生媒体连接状态更改。 例如，当适配器处于范围内（对于无线适配器）或用户连接网络电缆时，适配器会连接。

<a href="" id="ndis-status-media-disconnect"></a>\_媒体\_断开连接的 NDIS\_状态  
指示媒体连接状态从 "已连接" 更改为 "已断开连接"。 当连接的适配器失去网络连接时，会发生媒体断开连接状态更改。 例如，适配器失去连接，因为它超出范围（适用于无线适配器）或用户断开网络电缆。

除非另行指定，否则微型端口驱动程序应在检测状态更改后的两秒内显示媒体连接状态更改。

小型端口驱动程序可以在执行某些操作时检查媒体连接状态（请参阅以下列表）。 如果在操作完成后状态为 "已完成"，则微型端口驱动程序无需报告在操作过程中可能发生的任何状态更改。

以下列表描述了指示微型端口驱动程序的媒体连接状态更改的其他要求：

<a href="" id="resetting"></a>重置  
NDIS 调用[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)来重置微型端口驱动程序。 微型端口驱动程序可以同步或异步地完成重置。

如果重置后媒体连接状态不同，则驱动程序应在完成重置后两秒钟内显示状态。

小型端口驱动程序不应完成重置操作，直到它确定媒体连接状态。

<a href="" id="halting"></a>停止  
当 NDIS 调用[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)时，微型端口驱动程序不能指示任何媒体连接状态更改。

<a href="" id="initializing"></a>出错  
NDIS 调用微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数来初始化适配器。 在适配器初始化期间，微型端口驱动程序必须遵循以下准则：

-   如果在从*MiniportInitializeEx*返回后，微型端口驱动程序未指示媒体连接状态，ndis 将使用[**NDIS\_微型端口\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的**MEDIACONNECTSTATE**成员的值\_常规\_属性结构来确定媒体连接状态。 当驱动程序从其*MiniportInitializeEx*函数调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)时，微型端口驱动程序为 NDIS 提供此结构。

    **请注意**  如果将**MediaConnectState**成员设置为 MediaConnectStateUnknown，则在断开适配器连接时，NDIS 将继续。

     

-   如果在 NDIS 调用*MiniportInitializeEx*后连接了适配器，则微型端口驱动程序可以在从*MiniportInitializeEx*返回后的5秒内，指示 NDIS\_状态\_媒体\_连接。

-   如果在 NDIS 调用*MiniportInitializeEx*后适配器断开连接，则微型端口驱动程序应指示 NDIS\_状态\_\_MEDIA 在它从*MiniportInitializeEx*返回后2秒内断开连接。

-   初始化时，微型端口驱动程序应处理[OID\_代\_媒体\_连接\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-connect-status)或[oid\_生成\_共同\_媒体\_异步连接\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-media-connect-status)请求。 小型端口驱动程序在确定连接状态之前不应完成此类请求。

-   确定媒体连接状态不应延迟初始化。 如果需要，微型端口驱动程序应启动过程来确定*MiniportInitializeEx*中的连接状态，并在以后完成该过程。 例如，微型端口驱动程序可以设置计时器以轮询适配器的连接状态。

-   反序列化的微型端口驱动程序可以指示在初始化期间媒体断开连接，但不应使用序列化的微型端口驱动程序。

<a href="" id="sleeping"></a>等待  
当微型端口驱动程序收到[OID\_PNP\_集](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)时，它会进入网络睡眠状态，\_电源请求设置 D1、D2 或 D3 的设备电源状态。

微型端口驱动程序在进入睡眠状态或处于休眠状态时，不能指示任何媒体连接状态发生更改。

<a href="" id="waking"></a>唤醒  
当微型端口驱动程序收到 OID\_PNP 时，它将从睡眠状态唤醒\_设置\_电源请求，以将设备电源状态设置为 D0。

如果适配器在唤醒后的媒体连接状态与 "睡眠前" 状态相同，则微型端口驱动程序不应指示媒体连接状态更改。 如果连接状态发生更改，微型端口驱动程序应在唤醒后两秒钟内指示新的连接状态。

唤醒时，微型端口驱动程序应处理 OID\_代\_媒体\_连接\_状态或 OID\_生成\_共同\_媒体\_异步连接\_状态请求。 小型端口驱动程序在确定连接状态之前不应完成此类请求。

 

 





