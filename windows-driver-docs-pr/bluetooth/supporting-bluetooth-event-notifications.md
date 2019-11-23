---
title: 支持蓝牙事件通知
description: 支持蓝牙事件通知
ms.assetid: ddb6f1d4-0f6e-4b11-93fc-b0886d262749
keywords:
- 蓝牙 WDK，事件通知
- 事件通知 WDK 蓝牙
- 通知 WDK 蓝牙
- 配置文件驱动程序 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfb4cae3bee95ad5523df62294b2de24715875c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837536"
---
# <a name="supporting-bluetooth-event-notifications"></a>支持蓝牙事件通知


当配置文件驱动程序打开与远程设备的连接时，它应在连接关闭时或发生对连接的任何其他更改时，注册自己以获得通知。 此外，当配置文件驱动程序注册自身以接受传入连接时，它必须能够在远程设备尝试连接到该连接时收到通知。

使用面向同步连接的（SCO）连接的配置文件驱动程序实现并注册[*SCO 回调函数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)。 当客户端配置文件驱动程序请求连接到远程设备时，将注册相应的回调函数。

当 SCO 配置文件驱动程序发出**BRB\_SCO\_打开\_通道**BRB 时，它将指定一个指针，该指针指向在 BRB 对应的[ **\_BRB\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)\_\_**函数的回调**[*成员中。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback) 如果远程设备接受 SCO 连接请求，则当 SCO 连接发生变化时，蓝牙驱动程序堆栈可以通过回调函数向配置文件驱动程序发送通知。

有关创建 SCO 连接的详细信息，请参阅[创建与远程设备的 Sco 客户端连接](creating-a-sco-client-connection-to-a-remote-device.md)。

使用逻辑链接控制器和适配协议（L2CAP）连接的配置文件驱动程序实现并注册[*L2CAP 回调函数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)。

当 L2CAP 配置文件驱动程序发出**BRB\_L2CA\_打开\_通道**BRB 时，它将在 L2CAP 的相应[ **\_BRB\_BRB\_OPEN\_通道**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)结构的**回调**成员中指定一个指向其[*L2CA 回调函数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)的指针。 如果远程设备接受 L2CAP 连接请求，则在发生对 L2CAP 连接的更改时，蓝牙驱动程序堆栈可以通过回调函数向配置文件驱动程序发送通知。

有关创建 L2CAP 连接的详细信息，请参阅[创建与远程设备的 L2CAP 客户端连接](creating-a-l2cap-client-connection-to-a-remote-device.md)。

同样，当配置文件驱动程序注册自身以接受传入的（L2CAP，SCO）连接请求时，它必须注册一个回调函数，以便在远程设备尝试连接到该函数时收到通知。

使用 L2CAP 的配置文件驱动程序在[ **\_BRB\_L2CA\_REGISTER\_服务器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_register_server)结构的**IndicationCallback**成员中指定其[*L2CAP 回调函数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)。 然后，当远程设备尝试启动到配置文件驱动程序的 L2CAP 连接时，蓝牙驱动程序堆栈可以调用回调函数通知配置文件驱动程序。

使用 SCO 的配置文件驱动程序在[ **\_BRB\_SCO\_REGISTER\_服务器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_register_server)结构的**IndicationCallback**成员中指定其[*SCO 回调函数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)。 然后，当远程设备尝试启动到配置文件驱动程序的 SCO 连接时，蓝牙驱动程序堆栈可以调用回调函数以通知配置文件驱动程序。

配置文件驱动程序注册适当的回调函数后，如果在打开的连接中发生事件，则蓝牙驱动程序堆栈还可以通知配置文件驱动程序。

**请注意**  配置文件驱动程序可以注册同一个回调函数，以便向其发送有关打开的通道以及尝试连接到它的远程设备的更改通知。

 

对于 L2CAP 连接， [*L2CAP 回调函数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)接受三个参数：

-   为 L2CAP 连接定义的上下文。 对于 BRB\_L2CA\_注册\_服务器请求，此上下文为在 \_BRB 的**IndicationCallbackContext**成员中传递的值\_L2CA\_注册与请求传递的\_SERVER 结构。 对于**BRB\_L2CA\_打开\_通道**或**BRB\_L2CA\_打开\_通道\_响应**请求，此上下文是在 \_CallbackContext\_BRB 的**L2CA**成员中传递的值，\_\_与请求一起传递通道结构。

-   指示传入 L2CAP 连接或捆绑状态更改的通知事件类型的指示中的值[ **\_代码**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ne-bthddi-_indication_code)枚举。

-   一个指针，指向包含与通知事件相关联的参数[ **\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_indication_parameters)结构。

在[*L2CAP 回调函数的*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)*指示*参数中传递的值指定配置文件驱动程序应使用*参数参数的***参数**联合中的联合成员。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">如果<em>指示</em>参数的值等于 。</th>
<th align="left">...使用<em>Parameters</em>参数的以下联合成员</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>IndicationRemoteConnect</strong></p></td>
<td align="left"><p><strong>“连接”</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IndicationRemoteConfigRequest</strong></p></td>
<td align="left"><p><strong>ConfigRequest</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IndicationRemoteConfigResponse</strong></p></td>
<td align="left"><p><strong>ConfigResponse</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IndicationFreeExtraOptions</strong></p></td>
<td align="left"><p><strong>FreeExtraOptions</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IndicationRemoteDisconnect</strong></p></td>
<td align="left"><p><strong>取消</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IndicationRecvPacket</strong></p></td>
<td align="left"><p><strong>RecvPacket</strong></p></td>
</tr>
</tbody>
</table>

 

对于 SCO 连接， [*sco 回调函数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)接受三个参数：

-   为 SCO 连接定义的上下文。 对于**BRB\_SCO\_注册\_服务器**请求时，此上下文是在 \_BRB\_SCO\_的**IndicationCallbackContext**成员中传递的值。\_ 对于**BRB\_sco\_打开\_通道**或**BRB\_SCO\_打开\_通道\_响应**请求，此上下文是在 \_BRB\_SCO 的**CallbackContext**成员中传递的值。\_\_

-   [**SCO\_指示\_代码**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ne-bthddi-_sco_indication_code)枚举的值，该值指示传入 SCO 连接或捆绑状态更改通知的类型。

-   指向[**SCO\_指示\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_sco_indication_parameters)结构的指针，该结构包含与通知事件相关联的参数。

在[*SCO 回调函数的*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)*指示*参数中传递的值指定配置文件驱动程序应使用*参数参数在***参数**中的联合成员。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">如果<em>指示</em>参数的值等于 。</th>
<th align="left">...使用<em>Parameters</em>参数的以下联合成员</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ScoIndicationRemoteConnect</strong></p></td>
<td align="left"><p><strong>“连接”</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ScoIndicationRemoteDisconnect</strong></p></td>
<td align="left"><p><strong>取消</strong></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhandling_plug_and_play_removal_irpsspanspan-idhandling_plug_and_play_removal_irpsspanhandling-plug-and-play-removal-irps"></a><span id="handling_plug_and_play_removal_irps"></span><span id="HANDLING_PLUG_AND_PLAY_REMOVAL_IRPS"></span>处理即插即用删除 Irp

配置文件驱动程序应将所有[**IRP\_MN\_意外\_删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)irp 立即传递给蓝牙驱动程序堆栈处理。 请勿尝试在处理意外删除 IRP 的过程中关闭任何打开的通道。 接收到意外的删除 IRP 后，不要生成并发送任何将数据发送到基础广播的其他 BRBs。 但是，配置文件驱动程序可以在处理意外删除 IRP 时执行其他清理操作。

当蓝牙驱动程序堆栈接收到意外删除 IRP 后，它会将*ScoIndicationRemoteDisconnect*传递到配置文件驱动程序在配置文件驱动程序生成并发送 BRB\_sco 时由配置文件驱动程序指定的[*sco 回调函数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback) [ **\_打开\_通道**](https://docs.microsoft.com/previous-versions/ff536626(v=vs.85))或[**BRB\_SCO\_打开\_通道\_响应**](https://docs.microsoft.com/previous-versions/ff536627(v=vs.85))请求，以关闭当前打开的所有 SCO 通道。 同样，蓝牙驱动程序堆栈会将*IndicationRemoteDisconnect*传递到配置文件驱动程序在配置文件驱动程序生成并发送[**BRB\_L2CA\_打开\_通道**](https://docs.microsoft.com/previous-versions/ff536615(v=vs.85))或[**BRB\_L2CA\_打开\_通道\_响应**](https://docs.microsoft.com/previous-versions/ff536616(v=vs.85))请求时由配置文件驱动程序指定的[*L2CAP 回调函数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)，以关闭当前打开的任何 L2CAP 通道。

配置文件驱动程序在处理 IRP 时应取消注册所有服务器[ **\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)irp。 若要注销 SCO 服务器，配置文件驱动程序应[生成并发送](building-and-sending-a-brb.md) [**BRB\_SCO\_注销\_服务器**](https://docs.microsoft.com/previous-versions/ff536630(v=vs.85))请求。 若要注销 L2CAP 服务器，配置文件驱动程序应生成并发送[**BRB\_L2CA\_注销\_服务器**](https://docs.microsoft.com/previous-versions/ff536619(v=vs.85))请求。

 

 





