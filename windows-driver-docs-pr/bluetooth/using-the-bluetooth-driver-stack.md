---
title: 如何使用蓝牙驱动程序堆栈
description: 如何使用蓝牙驱动程序堆栈
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
ms.date: 07/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 014f124e75494acaf58f53a87ee7f20608545632
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608454"
---
# <a name="how-to-use-the-bluetooth-driver-stack"></a>如何使用蓝牙驱动程序堆栈


Windows 将加载并初始化蓝牙驱动程序堆栈后，驱动程序堆栈可发现活动已配对的蓝牙设备。 然后，驱动程序堆栈生成所有配对的设备的设备的标识符 （设备 Id）。 接下来，驱动程序堆栈使用标准和插即用 (PnP) 机制来加载每个设备的相应的配置文件驱动程序。 要加载的配置文件驱动程序已选择基于 INF 文件，用于安装配置文件驱动程序和设备标识符，如生成的蓝牙驱动程序堆栈和中所述[安装蓝牙设备](installing-a-bluetooth-device.md)。

与蓝牙驱动程序堆栈进行通信配置文件驱动程序通过使用基于 WDM 体系结构的所有驱动程序的标准基于 I/O 请求数据包 IRP 的机制。 通过分配并将关闭蓝牙驱动程序堆栈的 Irp 发送到蓝牙端口驱动程序，与其设备配置文件驱动程序通信*Bthport.sys*。

配置文件驱动程序分配并初始化由处理 Irp *Bthport.sys*。 配置文件驱动程序，然后使用传递到通过设备的 IOCTL 请求与他们的设备进行通信[ **IRP\_MJ\_内部\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)或[ **IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control) IRP。 配置文件驱动程序指定的 I/O 控制代码之一 IRP 的以下列表中。

内核模式调用方通过蓝牙驱动程序堆栈支持以下 Ioctl [ **IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control):

[**IOCTL\_同时为\_断开连接\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_disconnect_device)

[**IOCTL\_同时为\_获取\_设备\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_get_device_info)

[**IOCTL\_同时为\_获取\_本地\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_get_local_info)

[**IOCTL\_BTH\_GET\_RADIO\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_get_radio_info)

[**IOCTL\_BTH\_SDP\_ATTRIBUTE\_SEARCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_attribute_search)

[**IOCTL\_同时为\_SDP\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_connect)

[**IOCTL\_同时为\_SDP\_断开连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_disconnect)

[**IOCTL\_同时为\_SDP\_删除\_记录**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_remove_record)

[**IOCTL\_BTH\_SDP\_SERVICE\_ATTRIBUTE\_SEARCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_attribute_search)

[**IOCTL\_BTH\_SDP\_SERVICE\_SEARCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_search)

[**IOCTL\_同时为\_SDP\_提交\_记录**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record)

[**IOCTL\_同时为\_SDP\_提交\_记录\_WITH\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record_with_info)

蓝牙驱动程序堆栈支持以下 Ioctl 并[ **BRBs** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb)通过内核模式 （通常用于驱动程序的通信） 的调用方[ **IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control):

[**BRB\_HCI\_GET\_LOCAL\_BD\_ADDR**](https://docs.microsoft.com/previous-versions/ff536611(v=vs.85))

[**BRB\_L2CA\_REGISTER\_SERVER**](https://docs.microsoft.com/previous-versions/ff536618(v=vs.85))

[**BRB\_L2CA\_UNREGISTER\_SERVER**](https://docs.microsoft.com/previous-versions/ff536619(v=vs.85))

[**BRB\_L2CA\_OPEN\_CHANNEL**](https://docs.microsoft.com/previous-versions/ff536615(v=vs.85))

[**BRB\_L2CA\_开放\_通道\_响应**](https://docs.microsoft.com/previous-versions/ff536616(v=vs.85))

[**BRB\_L2CA\_CLOSE\_CHANNEL**](https://docs.microsoft.com/previous-versions/ff536614(v=vs.85))

[**BRB\_L2CA\_ACL\_TRANSFER**](https://docs.microsoft.com/previous-versions/ff536613(v=vs.85))

[**BRB\_L2CA\_UPDATE\_CHANNEL**](https://docs.microsoft.com/previous-versions/ff536620(v=vs.85))

[**BRB\_L2CA\_PING**](https://docs.microsoft.com/previous-versions/ff536617(v=vs.85))

[**BRB\_REGISTER\_PSM**](https://docs.microsoft.com/previous-versions/ff536621(v=vs.85))

[**BRB\_UNREGISTER\_PSM**](https://docs.microsoft.com/previous-versions/ff536632(v=vs.85))

[**BRB\_SCO\_REGISTER\_SERVER**](https://docs.microsoft.com/previous-versions/ff536628(v=vs.85))

[**BRB\_SCO\_UNREGISTER\_SERVER**](https://docs.microsoft.com/previous-versions/ff536630(v=vs.85))

[**BRB\_SCO\_OPEN\_CHANNEL**](https://docs.microsoft.com/previous-versions/ff536626(v=vs.85))

[**BRB\_SCO\_开放\_通道\_响应**](https://docs.microsoft.com/previous-versions/ff536627(v=vs.85))

[**BRB\_SCO\_CLOSE\_CHANNEL**](https://docs.microsoft.com/previous-versions/ff536622(v=vs.85))

[**BRB\_SCO\_TRANSFER**](https://docs.microsoft.com/previous-versions/ff536629(v=vs.85))

[**BRB\_SCO\_GET\_CHANNEL\_INFO**](https://docs.microsoft.com/previous-versions/ff536624(v=vs.85))

[**BRB\_SCO\_GET\_SYSTEM\_INFO**](https://docs.microsoft.com/previous-versions/ff536625(v=vs.85))

[**BRB\_SCO\_刷新\_通道**](https://docs.microsoft.com/previous-versions/ff536623(v=vs.85))

[**BRB\_ACL\_GET\_MODE**](https://docs.microsoft.com/previous-versions/ff536609(v=vs.85))

[**BRB\_ACL\_ENTER\_ACTIVE\_MODE**](https://docs.microsoft.com/previous-versions/ff536608(v=vs.85))

[**BRB\_GET\_DEVICE\_INTERFACE\_STRING**](https://docs.microsoft.com/previous-versions/ff536610(v=vs.85))

[**IOCTL\_INTERNAL\_BTH\_SUBMIT\_BRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_internal_bth_submit_brb)

[**IOCTL\_INTERNAL\_BTHENUM\_GET\_DEVINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_devinfo)

[**IOCTL\_INTERNAL\_BTHENUM\_GET\_ENUMINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_enuminfo)

有关如何使用 Ioctl 前面列表中所述的详细信息，请参阅[蓝牙 Ioctl](bluetooth-ioctls2.md)。

配置文件驱动程序主要使用 IOCTL\_内部\_同时为\_提交\_BRB 通信并蓝牙驱动程序堆栈中提供的功能与之交互。 配置文件驱动程序将使用 IOCTL\_内部\_同时为\_提交\_BRB 提供一种长度可变的数据结构称为蓝牙请求块 ( [ **BRB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb))到它所管理的设备。 配置文件驱动程序使用 BRBs 打开和关闭连接到远程设备并执行输入和输出的大多数任务。 IOCTL\_内部\_同时为\_提交\_BRB 包含 BRB 可进一步说明要执行的蓝牙操作。 若要了解有关如何生成和发送 BRBs 蓝牙驱动程序堆栈的详细信息，请参阅[生成和发送 BRB](building-and-sending-a-brb.md)。

每个 BRB 开头定义的标准标头[ **BRB\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_header)结构，它指定 BRB，确定 BRB 其余部分的结构的类型。 **类型**成员，必须等于中找到的值之一[ **BRB\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ne-bthddi-_brb_type)枚举，确定的蓝牙操作的类型，配置文件驱动程序请求。 BRB 结构和大小因 BRB 类型而异。 **长度**BRB 成员\_标头结构指定的大小，以字节为单位 BRB。 [ **BthAllocateBrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnbth_allocate_brb)， [ **BthInitializeBrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnbth_initialize_brb)，并[ **BthReuseBrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnbth_reuse_brb)函数将自动设置**类型**并**长度**成员。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_get_local_bd_addr" data-raw-source="[&lt;strong&gt;_BRB_GET_LOCAL_BD_ADDR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_get_local_bd_addr)"><strong>_BRB_GET_LOCAL_BD_ADDR</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_REGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_register_server" data-raw-source="[&lt;strong&gt;_BRB_L2CA_REGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_register_server)"><strong>_BRB_L2CA_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_unregister_server" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UNREGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_unregister_server)"><strong>_BRB_L2CA_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_open_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_open_channel)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_open_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_open_channel)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_close_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_CLOSE_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_close_channel)"><strong>_BRB_L2CA_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_ACL_TRANSFER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_acl_transfer" data-raw-source="[&lt;strong&gt;_BRB_L2CA_ACL_TRANSFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_acl_transfer)"><strong>_BRB_L2CA_ACL_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_UPDATE_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_update_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UPDATE_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_update_channel)"><strong>_BRB_L2CA_UPDATE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_PING</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_ping" data-raw-source="[&lt;strong&gt;_BRB_L2CA_PING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_ping)"><strong>_BRB_L2CA_PING</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_REGISTER_PSM</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_psm" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_psm)"><strong>_BRB_PSM</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_UNREGISTER_PSM</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_psm" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_psm)"><strong>_BRB_PSM</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_REGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_register_server" data-raw-source="[&lt;strong&gt;_BRB_SCO_REGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_register_server)"><strong>_BRB_SCO_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_unregister_server" data-raw-source="[&lt;strong&gt;_BRB_SCO_UNREGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_unregister_server)"><strong>_BRB_SCO_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_open_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_open_channel)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_open_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_open_channel)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_close_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_CLOSE_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_close_channel)"><strong>_BRB_SCO_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_TRANSFER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_transfer" data-raw-source="[&lt;strong&gt;_BRB_SCO_TRANSFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_transfer)"><strong>_BRB_SCO_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_GET_CHANNEL_INFO</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_get_channel_info" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_CHANNEL_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_get_channel_info)"><strong>_BRB_SCO_GET_CHANNEL_INFO</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_GET_SYSTEM_INFO</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_get_system_info" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_SYSTEM_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_get_system_info)"><strong>_BRB_SCO_GET_SYSTEM_INFO</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_FLUSH_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_flush_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_FLUSH_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_flush_channel)"><strong>_BRB_SCO_FLUSH_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_ACL_GET_MODE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_acl_get_mode" data-raw-source="[&lt;strong&gt;_BRB_ACL_GET_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_acl_get_mode)"><strong>_BRB_ACL_GET_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_ACL_ENTER_ACTIVE_MODE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_acl_enter_active_mode" data-raw-source="[&lt;strong&gt;_BRB_ACL_ENTER_ACTIVE_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_acl_enter_active_mode)"><strong>_BRB_ACL_ENTER_ACTIVE_MODE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_GET_DEVICE_INTERFACE_STRING</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_get_device_interface_string" data-raw-source="[&lt;strong&gt;_BRB_GET_DEVICE_INTERFACE_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_get_device_interface_string)"><strong>_BRB_GET_DEVICE_INTERFACE_STRING</strong></a></p></td>
</tr>
</tbody>
</table>

 

有关使用蓝牙 Ioctl 和 BRBs 的详细信息，请参阅[生成和发送 BRB](building-and-sending-a-brb.md)。

 

 





