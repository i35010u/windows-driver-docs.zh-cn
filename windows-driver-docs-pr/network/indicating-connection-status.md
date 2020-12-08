---
title: 指示连接状态
description: 指示连接状态
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
ms.openlocfilehash: 64823638813fc79f1787fec05bf9cbc49cee9861
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837937"
---
# <a name="indicating-connection-status"></a>指示连接状态





微型端口驱动程序调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 或 [**NdisMCoIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex) 以指示媒体连接状态的更改。 微型端口驱动程序将以下状态指示之一传递到 **NdisM (Co) IndicateStatus**：

<a href="" id="ndis-status-media-connect"></a>NDIS \_ 状态 \_ 媒体 \_ 连接  
指示媒体连接状态从 "已断开" 更改为 "已连接"。 如果断开连接的适配器建立网络连接，则会发生媒体连接状态更改。 例如，当适配器在无线适配器的 (范围内时，适配器将连接) 或用户连接网络电缆。

<a href="" id="ndis-status-media-disconnect"></a>NDIS \_ 状态 \_ 媒体 \_ 断开连接  
指示媒体连接状态从 "已连接" 更改为 "已断开连接"。 当连接的适配器失去网络连接时，会发生媒体断开连接状态更改。 例如，适配器失去连接，因为它超出无线适配器的范围 () 或用户断开网络电缆。

除非另行指定，否则微型端口驱动程序应在检测状态更改后的两秒内显示媒体连接状态更改。

小型端口驱动程序可以在执行某些操作时检查媒体连接状态 (参阅以下列表) 。 如果在操作完成后状态为 "已完成"，则微型端口驱动程序无需报告在操作过程中可能发生的任何状态更改。

以下列表描述了指示微型端口驱动程序的媒体连接状态更改的其他要求：

<a href="" id="resetting"></a>重置  
NDIS 调用 [*MiniportResetEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset) 来重置微型端口驱动程序。 微型端口驱动程序可以同步或异步地完成重置。

如果重置后媒体连接状态不同，则驱动程序应在完成重置后两秒钟内显示状态。

小型端口驱动程序不应完成重置操作，直到它确定媒体连接状态。

<a href="" id="halting"></a>停止  
当 NDIS 调用 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)时，微型端口驱动程序不能指示任何媒体连接状态更改。

<a href="" id="initializing"></a>正在初始化  
NDIS 调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数来初始化适配器。 在适配器初始化期间，微型端口驱动程序必须遵循以下准则：

-   如果微型端口驱动程序没有在从 *MiniportInitializeEx* 返回后显示媒体连接状态，ndis 将使用 [**ndis \_ 微型端口 \_ 适配器 \_ \_**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的 **MediaConnectState** 成员的值来确定媒体连接状态。 当驱动程序从其 *MiniportInitializeEx* 函数调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)时，微型端口驱动程序为 NDIS 提供此结构。

    **注意**  如果 **MediaConnectState** 成员设置为 MediaConnectStateUnknown，则 NDIS 将继续，就像适配器断开连接一样。

     

-   如果在 NDIS 调用 *MiniportInitializeEx* 后连接了适配器，微型端口驱动程序可以在 \_ \_ \_ 从 *MiniportInitializeEx* 返回后的5秒内指示 NDIS 状态媒体连接。

-   如果在 NDIS 调用 *MiniportInitializeEx* 后适配器断开连接，微型端口驱动程序应在 \_ \_ \_ 从 *MiniportInitializeEx* 返回后的2秒内将 NDIS 状态媒体断开连接。

-   初始化时，微型端口驱动程序应异步处理 [oid 生成 \_ \_ 媒体 \_ 连接 \_ 状态](./oid-gen-media-connect-status.md) 或 [oid 生成 \_ \_ CO \_ 媒体 \_ 连接 \_ 状态](./oid-gen-co-media-connect-status.md) 请求。 小型端口驱动程序在确定连接状态之前不应完成此类请求。

-   确定媒体连接状态不应延迟初始化。 如果需要，微型端口驱动程序应启动过程来确定 *MiniportInitializeEx* 中的连接状态，并在以后完成该过程。 例如，微型端口驱动程序可以设置计时器以轮询适配器的连接状态。

-   反序列化的微型端口驱动程序可以指示在初始化期间媒体断开连接，但不应使用序列化的微型端口驱动程序。

<a href="" id="sleeping"></a>Sleeping  
当微型端口驱动程序收到 [OID \_ PNP \_ 设置 \_ 电源](./oid-pnp-set-power.md) 请求以设置 D1、D2 或 D3 的设备电源状态时，它会进入网络睡眠状态。

微型端口驱动程序在进入睡眠状态或处于休眠状态时，不能指示任何媒体连接状态发生更改。

<a href="" id="waking"></a>唤醒  
当微型端口驱动程序收到 OID \_ PNP \_ 设置 \_ 电源请求以将设备电源状态设置为 D0 时，它会从睡眠状态唤醒。

如果适配器在唤醒后的媒体连接状态与 "睡眠前" 状态相同，则微型端口驱动程序不应指示媒体连接状态更改。 如果连接状态发生更改，微型端口驱动程序应在唤醒后两秒钟内指示新的连接状态。

唤醒时，微型端口驱动程序应异步处理 OID 生成 \_ \_ 媒体 \_ 连接 \_ 状态或 oid 生成 \_ \_ CO \_ 媒体 \_ 连接 \_ 状态请求。 小型端口驱动程序在确定连接状态之前不应完成此类请求。

 

