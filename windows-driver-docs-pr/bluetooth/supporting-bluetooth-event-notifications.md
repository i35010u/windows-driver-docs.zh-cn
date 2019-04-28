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
ms.openlocfilehash: d06d5b2c99fc62971f9dc99be5d44b6b7bd747cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328178"
---
# <a name="supporting-bluetooth-event-notifications"></a>支持蓝牙事件通知


当配置文件驱动程序将打开到远程设备的连接时，它应注册自身来关闭连接时，也可以连接到任何其他更改发生时收到通知。 此外，当配置文件驱动程序注册自己以接受传入的连接，它必须能够在远程设备尝试连接到它时收到通知。

使用 Synchronous Connection-Oriented (SCO) 连接的配置文件驱动程序实现和注册[ *SCO 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536772)。 请求连接到远程设备时，客户端配置文件驱动程序将注册相应的回调函数。

当 SCO 配置文件驱动程序发出**BRB\_SCO\_打开\_通道**BRB，它指定一个指向其[ *SCO 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536772)中**回调**BRB 的成员的相应[  **\_BRB\_SCO\_打开\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536870)结构。 如果远程设备接受 SCO 连接请求，蓝牙驱动程序堆栈可以将发送通知给通过回调函数的配置文件驱动程序到 SCO 连接发生更改时。

有关创建 SCO 连接的详细信息，请参阅[创建 SCO 客户端连接到远程设备](creating-a-sco-client-connection-to-a-remote-device.md)。

使用逻辑链接控制器和适应协议 (L2CAP) 连接的配置文件驱动程序实现和注册[ *L2CAP 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536755)。

当 L2CAP 配置文件驱动程序发出**BRB\_L2CA\_打开\_通道**BRB，它指定一个指向其[ *L2CAP 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536755)中**回调**BRB 的成员的相应[  **\_BRB\_L2CA\_打开\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536860)结构。 如果远程设备接受 L2CAP 连接请求，蓝牙驱动程序堆栈可以将发送通知给通过回调函数的配置文件驱动程序到 L2CAP 连接发生更改时。

有关创建 L2CAP 连接的详细信息，请参阅[创建 L2CAP 客户端连接到远程设备](creating-a-l2cap-client-connection-to-a-remote-device.md)。

同样，当配置文件驱动程序注册自己以接受传入的 （L2CAP、 SCO） 连接请求时，它必须注册一个回调函数来在远程设备尝试连接到它时收到通知。

使用 L2CAP 的配置文件驱动程序指定其[ *L2CAP 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536755)中**IndicationCallback**隶属[  **\_BRB\_L2CA\_注册\_SERVER** ](https://msdn.microsoft.com/library/windows/hardware/ff536862)结构。 蓝牙驱动程序堆栈然后可以调用的回调函数以在远程设备尝试启动 L2CAP 连接到配置文件驱动程序时通知配置文件驱动程序。

使用 SCO 的配置文件驱动程序指定其[ *SCO 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536772)中**IndicationCallback**隶属[  **\_BRB\_SCO\_注册\_SERVER** ](https://msdn.microsoft.com/library/windows/hardware/ff536871)结构。 蓝牙驱动程序堆栈然后可以调用的回调函数以在远程设备尝试启动 SCO 连接到配置文件驱动程序时通知配置文件驱动程序。

配置文件驱动程序注册相应的回调函数后，蓝牙驱动程序堆栈还可以通知配置文件驱动程序是否以及何时打开的连接上发生的事件。

**请注意**  配置文件驱动程序可以注册相同的回调函数，以将其发送更改通知有关打开的通道和有关尝试与其连接的远程设备。

 

为 L2CAP 连接[ *L2CAP 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536755)接受三个参数：

-   用于为 L2CAP 连接定义的上下文。 对于 BRB\_L2CA\_注册\_服务器请求时，此上下文是中传递的值**IndicationCallbackContext**隶属\_BRB\_L2CA\_注册\_服务器结构随请求一起传递。 情况下**BRB\_L2CA\_打开\_通道**或**BRB\_L2CA\_打开\_通道\_响应**请求时，此上下文是中传递的值**CallbackContext**的成员\_BRB\_L2CA\_打开\_通道结构随请求一起传递。

-   中的值[**指示\_代码**](https://msdn.microsoft.com/library/windows/hardware/ff536679)枚举，它指示传入的 L2CAP 连接或捆绑状态更改的通知事件的类型。

-   一个指向[**指示\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff536680)结构，其中包含与通知事件相关联的参数。

传入的值[ *L2CAP 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536755)*指示*参数指定的联合成员中**参数**联合的*参数*配置文件驱动程序应使用的参数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">如果的值<em>指示</em>参数等于...</th>
<th align="left">...使用以下的联合成员<em>参数</em>参数</th>
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
<td align="left"><p><strong>断开连接</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IndicationRecvPacket</strong></p></td>
<td align="left"><p><strong>RecvPacket</strong></p></td>
</tr>
</tbody>
</table>

 

SCO 连接[ *SCO 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536772)接受三个参数：

-   定义 SCO 连接上下文。 情况下**BRB\_SCO\_注册\_SERVER**请求时，此上下文是中传递的值**IndicationCallbackContext** 成员\_BRB\_SCO\_注册\_服务器结构随请求一起传递。 情况下**BRB\_SCO\_打开\_通道**或**BRB\_SCO\_打开\_通道\_响应**请求时，此上下文是中传递的值**CallbackContext**的成员\_BRB\_SCO\_打开\_通道结构随请求一起传递。

-   中的值[ **SCO\_指示\_代码**](https://msdn.microsoft.com/library/windows/hardware/ff536776)枚举，它指示传入的 SCO 连接或捆绑状态更改的通知的类型。

-   一个指向[ **SCO\_指示\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff536779)结构，其中包含与通知事件相关联的参数。

传入的值[ *SCO 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536772)*指示*参数指定的联合成员中**参数**联合*参数*配置文件驱动程序应使用的参数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">如果的值<em>指示</em>参数等于...</th>
<th align="left">...使用以下的联合成员<em>参数</em>参数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ScoIndicationRemoteConnect</strong></p></td>
<td align="left"><p><strong>“连接”</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ScoIndicationRemoteDisconnect</strong></p></td>
<td align="left"><p><strong>断开连接</strong></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhandlingplugandplayremovalirpsspanspan-idhandlingplugandplayremovalirpsspanhandling-plug-and-play-removal-irps"></a><span id="handling_plug_and_play_removal_irps"></span><span id="HANDLING_PLUG_AND_PLAY_REMOVAL_IRPS"></span>处理插删除 Irp

配置文件的驱动程序应通过所有[ **IRP\_MN\_惊讶\_删除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)堆栈的下层的 Irp 立即要处理的蓝牙驱动程序堆栈。 不要尝试关闭任何打开的通道处理意外删除 IRP 的过程。 不要生成和发送收到意外删除 IRP 后将数据发送到基础单选任何进一步 BRBs。 但是，配置文件驱动程序可以处理意外删除 IRP 时执行其他清理。

蓝牙驱动程序堆栈接收 IRP 被意外删除后，它将通过*ScoIndicationRemoteDisconnect*到[ *SCO 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536772)指定配置文件驱动程序配置文件驱动程序生成并发送[ **BRB\_SCO\_打开\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536626)或[ **BRB\_SCO\_打开\_通道\_响应**](https://msdn.microsoft.com/library/windows/hardware/ff536627)请求，以关闭当前打开任何 SCO 通道。 同样，将通过蓝牙驱动程序堆栈*IndicationRemoteDisconnect*到[ *L2CAP 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536755)指定配置文件驱动程序时配置文件驱动程序生成和发送[ **BRB\_L2CA\_打开\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536615)或[ **BRB\_L2CA\_打开\_通道\_响应**](https://msdn.microsoft.com/library/windows/hardware/ff536616)请求，以关闭当前打开任何 L2CAP 通道。

处理时，配置文件驱动程序应取消注册所有服务器[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738) Irp。 若要取消注册 SCO 服务器，配置文件驱动程序应[生成并发送](building-and-sending-a-brb.md) [ **BRB\_SCO\_注销\_服务器**](https://msdn.microsoft.com/library/windows/hardware/ff536630)请求。 若要注销 L2CAP 服务器，配置文件驱动程序应生成并发送[ **BRB\_L2CA\_注销\_SERVER** ](https://msdn.microsoft.com/library/windows/hardware/ff536619)请求。

 

 





