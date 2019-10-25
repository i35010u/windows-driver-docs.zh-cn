---
title: 如何使用蓝牙驱动程序堆栈
description: 如何使用蓝牙驱动程序堆栈
ms.assetid: c8a68c30-4cd6-4ee2-a653-7e0c1a28f4cf
keywords:
- 蓝牙 WDK，驱动程序堆栈
- 驱动程序堆栈 WDK 蓝牙
- 堆积 WDK 蓝牙
- 即插即用 WDK 蓝牙
- PnP WDK 蓝牙
- Irp WDK 蓝牙
- 配置文件驱动程序 WDK 蓝牙
- IOCTL_INTERNAL_BTH_SUBMIT_BRB
- 蓝牙 WDK，蓝牙请求块
- BRBs WDK
- 蓝牙请求阻止 WDK
- IRP_MJ_DEVICE_CONTROL
- IRP_MJ_INTERNAL_DEVICE_CONTROL
- 蓝牙 WDK，IOCTLs
- IOCTLs WDK 蓝牙
- 远程连接 WDK 蓝牙
- 连接 WDK 蓝牙
ms.date: 07/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82a2b47ccee646e5136fa4dd414e0c083141fd14
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834506"
---
# <a name="how-to-use-the-bluetooth-driver-stack"></a>如何使用蓝牙驱动程序堆栈


Windows 加载并初始化蓝牙驱动程序堆栈后，驱动程序堆栈会发现已经配对的活动蓝牙设备。 然后，驱动程序堆栈会为所有配对设备生成设备标识符（设备 Id）。 接下来，驱动程序堆栈使用标准即插即用（PnP）机制为每个设备加载适当的配置文件驱动程序。 选择要加载的配置文件驱动程序时，将基于安装配置文件驱动程序的 INF 文件和设备标识符（由蓝牙驱动程序堆栈生成并在[安装蓝牙设备](installing-a-bluetooth-device.md)中介绍）。

配置文件驱动程序通过基于 WDM 体系结构的所有驱动程序使用的标准 i/o 请求数据包（IRP）机制与蓝牙驱动程序堆栈进行通信。 配置文件驱动程序通过在蓝牙驱动程序堆栈上分配和发送 Irp 来与其设备通信，并将其发送到蓝牙端口驱动程序*Bthport。*

配置文件驱动程序分配并初始化要由*Bthport*处理的 irp。 然后，配置文件驱动程序使用通过 IRP\_MJ 发送到设备的 IOCTL 请求与设备进行通信，该请求通过[**IRP\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)或[**IRP\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)IRP。 配置文件驱动程序指定 IRP 中以下列表中的一个 i/o 控制代码。

蓝牙驱动程序堆栈通过[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)支持以下针对内核模式调用方的 IOCTLs：

[**IOCTL\_BTH\_断开\_设备的连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_disconnect_device)

[**IOCTL\_BTH\_获取\_设备\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_device_info)

[**IOCTL\_BTH\_获取\_本地\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_local_info)

[**IOCTL\_BTH\_获取\_无线电\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_radio_info)

[**IOCTL\_BTH\_SDP\_属性\_搜索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_attribute_search)

[**IOCTL\_BTH\_SDP\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_connect)

[**IOCTL\_BTH\_SDP\_断开连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_disconnect)

[**IOCTL\_BTH\_SDP\_删除\_记录**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_remove_record)

[**IOCTL\_BTH\_SDP\_服务\_属性\_搜索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_attribute_search)

[**IOCTL\_BTH\_SDP\_服务\_搜索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_search)

[**IOCTL\_BTH\_SDP\_提交\_记录**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record)

[**IOCTL\_BTH\_SDP\_提交\_记录\_\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record_with_info)

蓝牙驱动程序堆栈通过[**IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)，支持以下 IOCTLs 和[**BRBs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb)内核模式调用方（通常用于驱动程序到驱动程序通信）：

[**BRB\_HCI\_获取\_本地\_BD\_地址**](https://docs.microsoft.com/previous-versions/ff536611(v=vs.85))

[**BRB\_L2CA\_注册\_服务器**](https://docs.microsoft.com/previous-versions/ff536618(v=vs.85))

[**BRB\_L2CA\_注销\_服务器**](https://docs.microsoft.com/previous-versions/ff536619(v=vs.85))

[**BRB\_L2CA\_打开\_通道**](https://docs.microsoft.com/previous-versions/ff536615(v=vs.85))

[**BRB\_L2CA\_打开\_通道\_响应**](https://docs.microsoft.com/previous-versions/ff536616(v=vs.85))

[**BRB\_L2CA\_关闭\_通道**](https://docs.microsoft.com/previous-versions/ff536614(v=vs.85))

[**BRB\_L2CA\_ACL\_传输**](https://docs.microsoft.com/previous-versions/ff536613(v=vs.85))

[**BRB\_L2CA\_更新\_通道**](https://docs.microsoft.com/previous-versions/ff536620(v=vs.85))

[**BRB\_L2CA\_PING**](https://docs.microsoft.com/previous-versions/ff536617(v=vs.85))

[**BRB\_REGISTER\_PSM**](https://docs.microsoft.com/previous-versions/ff536621(v=vs.85))

[**BRB\_注销 PSM\_** ](https://docs.microsoft.com/previous-versions/ff536632(v=vs.85))

[**BRB\_SCO\_注册\_服务器**](https://docs.microsoft.com/previous-versions/ff536628(v=vs.85))

[**BRB\_SCO\_注销\_服务器**](https://docs.microsoft.com/previous-versions/ff536630(v=vs.85))

[**BRB\_SCO\_开放式\_通道**](https://docs.microsoft.com/previous-versions/ff536626(v=vs.85))

[**BRB\_SCO\_开放式\_通道\_响应**](https://docs.microsoft.com/previous-versions/ff536627(v=vs.85))

[**BRB\_SCO\_关闭\_通道**](https://docs.microsoft.com/previous-versions/ff536622(v=vs.85))

[**BRB\_SCO\_传输**](https://docs.microsoft.com/previous-versions/ff536629(v=vs.85))

[**BRB\_SCO\_获取\_通道\_信息**](https://docs.microsoft.com/previous-versions/ff536624(v=vs.85))

[**BRB\_SCO\_获取\_系统\_信息**](https://docs.microsoft.com/previous-versions/ff536625(v=vs.85))

[**BRB\_SCO\_刷新\_通道**](https://docs.microsoft.com/previous-versions/ff536623(v=vs.85))

[**BRB\_ACL\_获取\_模式**](https://docs.microsoft.com/previous-versions/ff536609(v=vs.85))

[**BRB\_ACL\_进入\_ACTIVE\_模式**](https://docs.microsoft.com/previous-versions/ff536608(v=vs.85))

[**BRB\_获取\_设备\_接口\_字符串**](https://docs.microsoft.com/previous-versions/ff536610(v=vs.85))

[**IOCTL\_内部\_BTH\_提交\_BRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bth_submit_brb)

[**IOCTL\_内部\_BTHENUM\_获取\_LNK-DEVINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_devinfo)

[**IOCTL\_内部\_BTHENUM\_获取\_ENUMINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_enuminfo)

有关如何使用前面列表中描述的 IOCTLs 的详细信息，请参阅[蓝牙 IOCTLs](bluetooth-ioctls2.md)。

配置文件驱动程序主要使用 IOCTL\_内部\_BTH\_提交\_BRB 来与蓝牙驱动程序堆栈中提供的功能通信和交互。 配置文件驱动程序使用 IOCTL\_内部\_BTH\_提交\_BRB，将称为 "蓝牙请求阻止" （ [**BRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb)）的可变长度数据结构传递到它所管理的设备。 配置文件驱动程序使用 BRBs 打开和关闭与远程设备的连接，并执行大部分输入和输出任务。 IOCTL\_内部\_BTH\_提交\_BRB 包含一个 BRB，该进一步说明了要执行的蓝牙操作。 若要详细了解如何在蓝牙驱动程序堆栈上构建和发送 BRBs，请参阅[生成和发送 BRB](building-and-sending-a-brb.md)。

每个 BRB 都以[**BRB\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_header)结构定义的标准标头开始，该标头结构指定 BRB 的类型，它确定了 BRB 的其余部分的结构。 **类型**成员（必须等于[**BRB\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ne-bthddi-_brb_type)枚举中找到的值之一）确定配置文件驱动程序请求的蓝牙操作的类型。 BRB 结构和大小因 BRB 类型的不同而异。 BRB\_标头结构的**Length**成员指定 BRB 的大小（以字节为单位）。 [**BthAllocateBrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_allocate_brb)、 [**BthInitializeBrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_initialize_brb)和[**BthReuseBrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_reuse_brb)函数自动设置**类型**和**长度**成员。

例如，若要打开与远程设备的连接，请指定一个函数代码， **BRB\_L2CA\_打开\_通道**或 BRB\_SCO\_打开\_通道，以指示配置文件驱动程序正在尝试打开到远程设备的 L2CAP 或 SCO 连接通道。 蓝牙驱动程序堆栈使用 BRB 结构的**Status**成员返回特定于蓝牙的状态代码。

对于每个 BRB，配置文件驱动程序必须通过要执行的蓝牙操作的相关信息分配和初始化相应的相应结构。

下表描述了与配置文件驱动程序可发出的特定 BRBs 对应的结构：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">蓝牙请求块（BRB）</th>
<th align="left">对应的结构</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BRB_HCI_GET_LOCAL_BD_ADDR</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_get_local_bd_addr" data-raw-source="[&lt;strong&gt;_BRB_GET_LOCAL_BD_ADDR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_get_local_bd_addr)"><strong>_BRB_GET_LOCAL_BD_ADDR</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_REGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_register_server" data-raw-source="[&lt;strong&gt;_BRB_L2CA_REGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_register_server)"><strong>_BRB_L2CA_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_unregister_server" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UNREGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_unregister_server)"><strong>_BRB_L2CA_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_close_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_CLOSE_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_close_channel)"><strong>_BRB_L2CA_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_ACL_TRANSFER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_acl_transfer" data-raw-source="[&lt;strong&gt;_BRB_L2CA_ACL_TRANSFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_acl_transfer)"><strong>_BRB_L2CA_ACL_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_UPDATE_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_update_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UPDATE_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_update_channel)"><strong>_BRB_L2CA_UPDATE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_PING</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_ping" data-raw-source="[&lt;strong&gt;_BRB_L2CA_PING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_ping)"><strong>_BRB_L2CA_PING</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_REGISTER_PSM</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm)"><strong>_BRB_PSM</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_UNREGISTER_PSM</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm)"><strong>_BRB_PSM</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_REGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_register_server" data-raw-source="[&lt;strong&gt;_BRB_SCO_REGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_register_server)"><strong>_BRB_SCO_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_unregister_server" data-raw-source="[&lt;strong&gt;_BRB_SCO_UNREGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_unregister_server)"><strong>_BRB_SCO_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_close_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_CLOSE_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_close_channel)"><strong>_BRB_SCO_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_TRANSFER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_transfer" data-raw-source="[&lt;strong&gt;_BRB_SCO_TRANSFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_transfer)"><strong>_BRB_SCO_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_GET_CHANNEL_INFO</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_get_channel_info" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_CHANNEL_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_get_channel_info)"><strong>_BRB_SCO_GET_CHANNEL_INFO</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_GET_SYSTEM_INFO</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_get_system_info" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_SYSTEM_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_get_system_info)"><strong>_BRB_SCO_GET_SYSTEM_INFO</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_FLUSH_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_flush_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_FLUSH_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_flush_channel)"><strong>_BRB_SCO_FLUSH_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_ACL_GET_MODE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_acl_get_mode" data-raw-source="[&lt;strong&gt;_BRB_ACL_GET_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_acl_get_mode)"><strong>_BRB_ACL_GET_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_ACL_ENTER_ACTIVE_MODE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_acl_enter_active_mode" data-raw-source="[&lt;strong&gt;_BRB_ACL_ENTER_ACTIVE_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_acl_enter_active_mode)"><strong>_BRB_ACL_ENTER_ACTIVE_MODE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_GET_DEVICE_INTERFACE_STRING</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_get_device_interface_string" data-raw-source="[&lt;strong&gt;_BRB_GET_DEVICE_INTERFACE_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_get_device_interface_string)"><strong>_BRB_GET_DEVICE_INTERFACE_STRING</strong></a></p></td>
</tr>
</tbody>
</table>

 

有关使用蓝牙 IOCTLs 和 BRBs 的详细信息，请参阅[生成和发送 BRB](building-and-sending-a-brb.md)。

 

 





