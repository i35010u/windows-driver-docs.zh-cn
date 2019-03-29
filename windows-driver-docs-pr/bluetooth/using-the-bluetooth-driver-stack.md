---
title: 使用蓝牙驱动程序堆栈
description: 使用蓝牙驱动程序堆栈
ms.assetid: c8a68c30-4cd6-4ee2-a653-7e0c1a28f4cf
keywords:
- 蓝牙 WDK，驱动程序堆栈
- 驱动程序堆栈 WDK 蓝牙
- 堆栈 WDK 蓝牙
- Plug and Play WDK 蓝牙
- 即插即用 WDK 蓝牙
- Irp WDK 蓝牙
- 配置文件驱动程序 WDK 蓝牙
- IOCTL_INTERNAL_BTH_SUBMIT_BRB
- 蓝牙 WDK、 蓝牙请求块
- BRBs WDK
- 蓝牙请求块 WDK
- IRP_MJ_DEVICE_CONTROL
- IRP_MJ_INTERNAL_DEVICE_CONTROL
- 蓝牙 WDK Ioctl
- Ioctl WDK 蓝牙
- 远程连接 WDK 蓝牙
- 连接 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a6441c861987621cee2c56dc0d7188db4cc2902
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563064"
---
# <a name="using-the-bluetooth-driver-stack"></a>使用蓝牙驱动程序堆栈


Windows 将加载并初始化蓝牙驱动程序堆栈后，驱动程序堆栈可发现活动已配对的蓝牙设备。 然后，驱动程序堆栈生成所有配对的设备的设备的标识符 （设备 Id）。 接下来，驱动程序堆栈使用标准和插即用 (PnP) 机制来加载每个设备的相应的配置文件驱动程序。 要加载的配置文件驱动程序已选择基于 INF 文件，用于安装配置文件驱动程序和设备标识符，如生成的蓝牙驱动程序堆栈和中所述[安装蓝牙设备](installing-a-bluetooth-device.md)。

与蓝牙驱动程序堆栈进行通信配置文件驱动程序通过使用基于 WDM 体系结构的所有驱动程序的标准基于 I/O 请求数据包 IRP 的机制。 通过分配并将关闭蓝牙驱动程序堆栈的 Irp 发送到蓝牙端口驱动程序，与其设备配置文件驱动程序通信*Bthport.sys*。

配置文件驱动程序分配并初始化由处理 Irp *Bthport.sys*。 配置文件驱动程序，然后使用传递到通过设备的 IOCTL 请求与他们的设备进行通信[ **IRP\_MJ\_内部\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550766)或[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744) IRP。 配置文件驱动程序指定的 I/O 控制代码之一 IRP 的以下列表中。

内核模式调用方通过蓝牙驱动程序堆栈支持以下 Ioctl [ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744):

[**IOCTL\_同时为\_断开连接\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff536682)

[**IOCTL\_同时为\_获取\_设备\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff536683)

[**IOCTL\_同时为\_获取\_本地\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff536684)

[**IOCTL\_BTH\_GET\_RADIO\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff536685)

[**IOCTL\_BTH\_SDP\_ATTRIBUTE\_SEARCH**](https://msdn.microsoft.com/library/windows/hardware/ff536687)

[**IOCTL\_同时为\_SDP\_连接**](https://msdn.microsoft.com/library/windows/hardware/ff536688)

[**IOCTL\_同时为\_SDP\_断开连接**](https://msdn.microsoft.com/library/windows/hardware/ff536689)

[**IOCTL\_同时为\_SDP\_删除\_记录**](https://msdn.microsoft.com/library/windows/hardware/ff536690)

[**IOCTL\_BTH\_SDP\_SERVICE\_ATTRIBUTE\_SEARCH**](https://msdn.microsoft.com/library/windows/hardware/ff536691)

[**IOCTL\_BTH\_SDP\_SERVICE\_SEARCH**](https://msdn.microsoft.com/library/windows/hardware/ff536692)

[**IOCTL\_同时为\_SDP\_提交\_记录**](https://msdn.microsoft.com/library/windows/hardware/ff536693)

[**IOCTL\_同时为\_SDP\_提交\_记录\_WITH\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff536694)

蓝牙驱动程序堆栈支持以下 Ioctl 并[ **BRBs** ](https://msdn.microsoft.com/library/windows/hardware/ff536607)通过内核模式 （通常用于驱动程序的通信） 的调用方[ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766):

[**BRB\_HCI\_GET\_LOCAL\_BD\_ADDR**](https://msdn.microsoft.com/library/windows/hardware/ff536611)

[**BRB\_L2CA\_REGISTER\_SERVER**](https://msdn.microsoft.com/library/windows/hardware/ff536618)

[**BRB\_L2CA\_UNREGISTER\_SERVER**](https://msdn.microsoft.com/library/windows/hardware/ff536619)

[**BRB\_L2CA\_OPEN\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/ff536615)

[**BRB\_L2CA\_开放\_通道\_响应**](https://msdn.microsoft.com/library/windows/hardware/ff536616)

[**BRB\_L2CA\_CLOSE\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/ff536614)

[**BRB\_L2CA\_ACL\_TRANSFER**](https://msdn.microsoft.com/library/windows/hardware/ff536613)

[**BRB\_L2CA\_UPDATE\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/ff536620)

[**BRB\_L2CA\_PING**](https://msdn.microsoft.com/library/windows/hardware/ff536617)

[**BRB\_REGISTER\_PSM**](https://msdn.microsoft.com/library/windows/hardware/ff536621)

[**BRB\_UNREGISTER\_PSM**](https://msdn.microsoft.com/library/windows/hardware/ff536632)

[**BRB\_SCO\_REGISTER\_SERVER**](https://msdn.microsoft.com/library/windows/hardware/ff536628)

[**BRB\_SCO\_UNREGISTER\_SERVER**](https://msdn.microsoft.com/library/windows/hardware/ff536630)

[**BRB\_SCO\_OPEN\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/ff536626)

[**BRB\_SCO\_开放\_通道\_响应**](https://msdn.microsoft.com/library/windows/hardware/ff536627)

[**BRB\_SCO\_CLOSE\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/ff536622)

[**BRB\_SCO\_TRANSFER**](https://msdn.microsoft.com/library/windows/hardware/ff536629)

[**BRB\_SCO\_GET\_CHANNEL\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff536624)

[**BRB\_SCO\_GET\_SYSTEM\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff536625)

[**BRB\_SCO\_刷新\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536623)

[**BRB\_ACL\_GET\_MODE**](https://msdn.microsoft.com/library/windows/hardware/ff536609)

[**BRB\_ACL\_ENTER\_ACTIVE\_MODE**](https://msdn.microsoft.com/library/windows/hardware/ff536608)

[**BRB\_GET\_DEVICE\_INTERFACE\_STRING**](https://msdn.microsoft.com/library/windows/hardware/ff536610)

[**IOCTL\_INTERNAL\_BTH\_SUBMIT\_BRB**](https://msdn.microsoft.com/library/windows/hardware/ff536751)

[**IOCTL\_INTERNAL\_BTHENUM\_GET\_DEVINFO**](https://msdn.microsoft.com/library/windows/hardware/ff536748)

[**IOCTL\_INTERNAL\_BTHENUM\_GET\_ENUMINFO**](https://msdn.microsoft.com/library/windows/hardware/ff536750)

有关如何使用 Ioctl 前面列表中所述的详细信息，请参阅[蓝牙 Ioctl](bluetooth-ioctls2.md)。

配置文件驱动程序主要使用 IOCTL\_内部\_同时为\_提交\_BRB 通信并蓝牙驱动程序堆栈中提供的功能与之交互。 配置文件驱动程序将使用 IOCTL\_内部\_同时为\_提交\_BRB 提供一种长度可变的数据结构称为蓝牙请求块 ( [ **BRB** ](https://msdn.microsoft.com/library/windows/hardware/ff536607))到它所管理的设备。 配置文件驱动程序使用 BRBs 打开和关闭连接到远程设备并执行输入和输出的大多数任务。 IOCTL\_内部\_同时为\_提交\_BRB 包含 BRB 可进一步说明要执行的蓝牙操作。 若要了解有关如何生成和发送 BRBs 蓝牙驱动程序堆栈的详细信息，请参阅[生成和发送 BRB](building-and-sending-a-brb.md)。

每个 BRB 开头定义的标准标头[ **BRB\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff536612)结构，它指定 BRB，确定 BRB 其余部分的结构的类型。 **类型**成员，必须等于中找到的值之一[ **BRB\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff536631)枚举，确定的蓝牙操作的类型，配置文件驱动程序请求。 BRB 结构和大小因 BRB 类型而异。 **长度**BRB 成员\_标头结构指定的大小，以字节为单位 BRB。 [ **BthAllocateBrb**](https://msdn.microsoft.com/library/windows/hardware/ff536634)， [ **BthInitializeBrb**](https://msdn.microsoft.com/library/windows/hardware/ff536639)，并[ **BthReuseBrb**](https://msdn.microsoft.com/library/windows/hardware/ff536640)函数将自动设置**类型**并**长度**成员。

例如，若要打开到远程设备的连接，请指定函数代码中的任一**BRB\_L2CA\_打开\_通道**或 BRB\_SCO\_打开\_通道，以指示配置文件驱动程序尝试打开 L2CAP 或远程设备的 SCO 连接通道。 使用蓝牙驱动程序堆栈**状态**BRB 结构的成员，才能返回特定于蓝牙的状态代码。

对于每个 BRB 配置文件驱动程序必须分配并初始化适当的相应结构与要执行的蓝牙操作有关的信息。

下表描述对应于配置文件驱动程序可以发出的特定 BRBs 的结构：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">蓝牙请求块 (BRB)</th>
<th align="left">相应的结构</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BRB_HCI_GET_LOCAL_BD_ADDR</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536857" data-raw-source="[&lt;strong&gt;_BRB_GET_LOCAL_BD_ADDR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536857)"><strong>_BRB_GET_LOCAL_BD_ADDR</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_REGISTER_SERVER</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536862" data-raw-source="[&lt;strong&gt;_BRB_L2CA_REGISTER_SERVER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536862)"><strong>_BRB_L2CA_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536863" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UNREGISTER_SERVER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536863)"><strong>_BRB_L2CA_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536860" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536860)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536860" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536860)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536859" data-raw-source="[&lt;strong&gt;_BRB_L2CA_CLOSE_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536859)"><strong>_BRB_L2CA_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_ACL_TRANSFER</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536858" data-raw-source="[&lt;strong&gt;_BRB_L2CA_ACL_TRANSFER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536858)"><strong>_BRB_L2CA_ACL_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_UPDATE_CHANNEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536864" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UPDATE_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536864)"><strong>_BRB_L2CA_UPDATE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_PING</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536861" data-raw-source="[&lt;strong&gt;_BRB_L2CA_PING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536861)"><strong>_BRB_L2CA_PING</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_REGISTER_PSM</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536865" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536865)"><strong>_BRB_PSM</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_UNREGISTER_PSM</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536865" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536865)"><strong>_BRB_PSM</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_REGISTER_SERVER</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536871" data-raw-source="[&lt;strong&gt;_BRB_SCO_REGISTER_SERVER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536871)"><strong>_BRB_SCO_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536873" data-raw-source="[&lt;strong&gt;_BRB_SCO_UNREGISTER_SERVER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536873)"><strong>_BRB_SCO_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536870" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536870)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536870" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536870)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536866" data-raw-source="[&lt;strong&gt;_BRB_SCO_CLOSE_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536866)"><strong>_BRB_SCO_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_TRANSFER</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536872" data-raw-source="[&lt;strong&gt;_BRB_SCO_TRANSFER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536872)"><strong>_BRB_SCO_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_GET_CHANNEL_INFO</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536868" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_CHANNEL_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536868)"><strong>_BRB_SCO_GET_CHANNEL_INFO</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_GET_SYSTEM_INFO</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536869" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_SYSTEM_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536869)"><strong>_BRB_SCO_GET_SYSTEM_INFO</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_FLUSH_CHANNEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536867" data-raw-source="[&lt;strong&gt;_BRB_SCO_FLUSH_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536867)"><strong>_BRB_SCO_FLUSH_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_ACL_GET_MODE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536855" data-raw-source="[&lt;strong&gt;_BRB_ACL_GET_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536855)"><strong>_BRB_ACL_GET_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_ACL_ENTER_ACTIVE_MODE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536854" data-raw-source="[&lt;strong&gt;_BRB_ACL_ENTER_ACTIVE_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536854)"><strong>_BRB_ACL_ENTER_ACTIVE_MODE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_GET_DEVICE_INTERFACE_STRING</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536856" data-raw-source="[&lt;strong&gt;_BRB_GET_DEVICE_INTERFACE_STRING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536856)"><strong>_BRB_GET_DEVICE_INTERFACE_STRING</strong></a></p></td>
</tr>
</tbody>
</table>

 

有关使用蓝牙 Ioctl 和 BRBs 的详细信息，请参阅[生成和发送 BRB](building-and-sending-a-brb.md)。

 

 





