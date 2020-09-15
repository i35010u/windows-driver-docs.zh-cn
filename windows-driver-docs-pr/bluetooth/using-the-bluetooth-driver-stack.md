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
ms.openlocfilehash: 8a9fa74a66a2fda3299790ae15c017c951b18bd6
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101536"
---
# <a name="how-to-use-the-bluetooth-driver-stack"></a>如何使用蓝牙驱动程序堆栈


Windows 加载并初始化蓝牙驱动程序堆栈后，驱动程序堆栈会发现已经配对的活动蓝牙设备。 然后，驱动程序堆栈会为所有配对设备)  (设备 Id 生成设备标识符。 接下来，驱动程序堆栈使用标准即插即用 (PnP) 机制为每个设备加载适当的配置文件驱动程序。 选择要加载的配置文件驱动程序时，将基于安装配置文件驱动程序的 INF 文件和设备标识符（由蓝牙驱动程序堆栈生成并在 [安装蓝牙设备](installing-a-bluetooth-device.md)中介绍）。

配置文件驱动程序通过标准 i/o 请求数据包与蓝牙驱动程序堆栈进行通信， (IRP 基于 WDM 体系结构的所有驱动程序所采用的基于) 的机制。 配置文件驱动程序通过在蓝牙驱动程序堆栈之间分配并将 Irp 发送到蓝牙端口驱动程序来与其设备通信， *Bthport.sys*。

配置文件驱动程序分配并初始化要由 *Bthport.sys*处理的 irp。 然后，配置文件驱动程序使用通过 [**IRP \_ mj \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md) 或 [**irp \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md) irp 传递到设备的 IOCTL 请求来与其设备通信。 配置文件驱动程序指定 IRP 中以下列表中的一个 i/o 控制代码。

蓝牙驱动程序堆栈通过 [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md)支持以下 IOCTLs 的内核模式调用方：

[**IOCTL \_ BTH \_ 断开 \_ 设备**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_disconnect_device)

[**IOCTL \_ BTH \_ 获取 \_ 设备 \_ 信息**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_device_info)

[**IOCTL \_ BTH \_ 获取 \_ 本地 \_ 信息**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_local_info)

[**IOCTL \_ BTH \_ 获取 \_ 无线电 \_ 信息**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_radio_info)

[**IOCTL \_ BTH \_ SDP \_ 特性 \_ 搜索**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_attribute_search)

[**IOCTL \_ BTH \_ SDP \_ 连接**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_connect)

[**IOCTL \_ BTH \_ SDP \_ 断开连接**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_disconnect)

[**IOCTL \_ BTH \_ SDP \_ 删除 \_ 记录**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_remove_record)

[**IOCTL \_ BTH \_ SDP \_ 服务 \_ 属性 \_ 搜索**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_attribute_search)

[**IOCTL \_ BTH \_ SDP \_ 服务 \_ 搜索**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_search)

[**IOCTL \_ BTH \_ SDP \_ 提交 \_ 记录**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record)

[**IOCTL \_ BTH \_ SDP \_ 提交 \_ 记录 \_ ，含 \_ 信息**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record_with_info)

蓝牙驱动程序堆栈支持以下 IOCTLs 和 [**BRBs**](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb) 内核模式调用方 (通常用于通过 [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md)的驱动程序到驱动程序通信) ：

[**BRB \_ HCI \_ 获取 \_ 本地 \_ BD \_ 地址**](/previous-versions/ff536611(v=vs.85))

[**BRB \_ L2CA \_ 注册 \_ 服务器**](/previous-versions/ff536618(v=vs.85))

[**BRB \_ L2CA \_ 注销 \_ 服务器**](/previous-versions/ff536619(v=vs.85))

[**BRB \_ L2CA \_ 开 \_ 通道**](/previous-versions/ff536615(v=vs.85))

[**BRB \_ L2CA \_ 打开 \_ 通道 \_ 响应**](/previous-versions/ff536616(v=vs.85))

[**BRB \_ L2CA \_ 闭合 \_ 通道**](/previous-versions/ff536614(v=vs.85))

[**BRB \_ L2CA \_ ACL \_ 传输**](/previous-versions/ff536613(v=vs.85))

[**BRB \_ L2CA \_ 更新 \_ 通道**](/previous-versions/ff536620(v=vs.85))

[**BRB \_ L2CA \_ PING**](/previous-versions/ff536617(v=vs.85))

[**BRB \_ 注册 \_ PSM**](/previous-versions/ff536621(v=vs.85))

[**BRB \_ 注销 \_ PSM**](/previous-versions/ff536632(v=vs.85))

[**BRB \_ SCO \_ 注册 \_ 服务器**](/previous-versions/ff536628(v=vs.85))

[**BRB \_ SCO \_ 注销 \_ 服务器**](/previous-versions/ff536630(v=vs.85))

[**BRB \_ SCO \_ 开放式 \_ 通道**](/previous-versions/ff536626(v=vs.85))

[**BRB \_ SCO \_ 打开 \_ 通道 \_ 响应**](/previous-versions/ff536627(v=vs.85))

[**BRB \_ SCO \_ 结束 \_ 通道**](/previous-versions/ff536622(v=vs.85))

[**BRB \_ SCO \_ 传输**](/previous-versions/ff536629(v=vs.85))

[**BRB \_ SCO \_ 获取 \_ 通道 \_ 信息**](/previous-versions/ff536624(v=vs.85))

[**BRB \_ SCO \_ 获取 \_ 系统 \_ 信息**](/previous-versions/ff536625(v=vs.85))

[**BRB \_ SCO \_ 刷新 \_ 通道**](/previous-versions/ff536623(v=vs.85))

[**BRB \_ ACL \_ 获取 \_ 模式**](/previous-versions/ff536609(v=vs.85))

[**BRB \_ ACL \_ 进入 \_ 活动 \_ 模式**](/previous-versions/ff536608(v=vs.85))

[**BRB \_ 获取 \_ 设备 \_ 接口 \_ 字符串**](/previous-versions/ff536610(v=vs.85))

[**IOCTL \_ 内部 \_ BTH \_ 提交 \_ BRB**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bth_submit_brb)

[**IOCTL \_ 内部 \_ BTHENUM \_ GET \_ LNK-DEVINFO**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_devinfo)

[**IOCTL \_ 内部 \_ BTHENUM \_ GET \_ ENUMINFO**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_enuminfo)

有关如何使用前面列表中描述的 IOCTLs 的详细信息，请参阅 [蓝牙 IOCTLs](bluetooth-ioctls2.md)。

配置文件驱动程序主要使用 IOCTL \_ 内部 \_ BTH \_ SUBMIT \_ BRB 来与蓝牙驱动程序堆栈中提供的功能进行通信和交互。 配置文件驱动程序使用 IOCTL \_ INTERNAL \_ BTH \_ SUBMIT \_ BRB 将长度可变的数据结构（称为蓝牙请求块）传递给它所管理的设备 ( [**BRB**](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb)) 。 配置文件驱动程序使用 BRBs 打开和关闭与远程设备的连接，并执行大部分输入和输出任务。 IOCTL \_ INTERNAL \_ BTH \_ SUBMIT \_ BRB 包含一个 BRB，它进一步说明了要执行的蓝牙操作。 若要详细了解如何在蓝牙驱动程序堆栈上构建和发送 BRBs，请参阅 [生成和发送 BRB](building-and-sending-a-brb.md)。

每个 BRB 都以 [**BRB \_ 标头**](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_header) 结构定义的标准标头开始，该标头结构指定 BRB 的类型，它确定了 BRB 的其余部分的结构。 **类型**成员（必须等于在[**BRB \_ 类型**](/windows-hardware/drivers/ddi/bthddi/ne-bthddi-_brb_type)枚举中找到的值之一）确定配置文件驱动程序请求的蓝牙操作的类型。 BRB 结构和大小因 BRB 类型的不同而异。 BRB **Length** \_ 标头结构的 LENGTH 成员指定 BRB 的大小（以字节为单位）。 [**BthAllocateBrb**](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_allocate_brb)、 [**BthInitializeBrb**](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_initialize_brb)和[**BthReuseBrb**](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_reuse_brb)函数自动设置**类型**和**长度**成员。

例如，若要打开与远程设备的连接，请指定一个函数代码（ **BRB \_ L2CA \_ OPEN \_ 通道** 或 BRB \_ SCO \_ 开放式 \_ 通道），以指示配置文件驱动程序正在尝试打开到远程设备的 L2CAP 或 SCO 连接通道。 蓝牙驱动程序堆栈使用 BRB 结构的 **Status** 成员返回特定于蓝牙的状态代码。

对于每个 BRB，配置文件驱动程序必须通过要执行的蓝牙操作的相关信息分配和初始化相应的相应结构。

下表描述了与配置文件驱动程序可发出的特定 BRBs 对应的结构：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">蓝牙请求块 (BRB) </th>
<th align="left">对应的结构</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BRB_HCI_GET_LOCAL_BD_ADDR</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_get_local_bd_addr" data-raw-source="[&lt;strong&gt;_BRB_GET_LOCAL_BD_ADDR&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_get_local_bd_addr)"><strong>_BRB_GET_LOCAL_BD_ADDR</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_REGISTER_SERVER</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_register_server" data-raw-source="[&lt;strong&gt;_BRB_L2CA_REGISTER_SERVER&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_register_server)"><strong>_BRB_L2CA_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_unregister_server" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UNREGISTER_SERVER&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_unregister_server)"><strong>_BRB_L2CA_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_close_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_CLOSE_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_close_channel)"><strong>_BRB_L2CA_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_ACL_TRANSFER</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_acl_transfer" data-raw-source="[&lt;strong&gt;_BRB_L2CA_ACL_TRANSFER&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_acl_transfer)"><strong>_BRB_L2CA_ACL_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_UPDATE_CHANNEL</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_update_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UPDATE_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_update_channel)"><strong>_BRB_L2CA_UPDATE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_PING</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_ping" data-raw-source="[&lt;strong&gt;_BRB_L2CA_PING&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_ping)"><strong>_BRB_L2CA_PING</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_REGISTER_PSM</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm)"><strong>_BRB_PSM</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_UNREGISTER_PSM</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm)"><strong>_BRB_PSM</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_REGISTER_SERVER</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_register_server" data-raw-source="[&lt;strong&gt;_BRB_SCO_REGISTER_SERVER&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_register_server)"><strong>_BRB_SCO_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_unregister_server" data-raw-source="[&lt;strong&gt;_BRB_SCO_UNREGISTER_SERVER&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_unregister_server)"><strong>_BRB_SCO_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_close_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_CLOSE_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_close_channel)"><strong>_BRB_SCO_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_TRANSFER</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_transfer" data-raw-source="[&lt;strong&gt;_BRB_SCO_TRANSFER&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_transfer)"><strong>_BRB_SCO_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_GET_CHANNEL_INFO</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_get_channel_info" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_CHANNEL_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_get_channel_info)"><strong>_BRB_SCO_GET_CHANNEL_INFO</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_GET_SYSTEM_INFO</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_get_system_info" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_SYSTEM_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_get_system_info)"><strong>_BRB_SCO_GET_SYSTEM_INFO</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_FLUSH_CHANNEL</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_flush_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_FLUSH_CHANNEL&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_flush_channel)"><strong>_BRB_SCO_FLUSH_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_ACL_GET_MODE</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_acl_get_mode" data-raw-source="[&lt;strong&gt;_BRB_ACL_GET_MODE&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_acl_get_mode)"><strong>_BRB_ACL_GET_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_ACL_ENTER_ACTIVE_MODE</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_acl_enter_active_mode" data-raw-source="[&lt;strong&gt;_BRB_ACL_ENTER_ACTIVE_MODE&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_acl_enter_active_mode)"><strong>_BRB_ACL_ENTER_ACTIVE_MODE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_GET_DEVICE_INTERFACE_STRING</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_get_device_interface_string" data-raw-source="[&lt;strong&gt;_BRB_GET_DEVICE_INTERFACE_STRING&lt;/strong&gt;](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_get_device_interface_string)"><strong>_BRB_GET_DEVICE_INTERFACE_STRING</strong></a></p></td>
</tr>
</tbody>
</table>

 

有关使用蓝牙 IOCTLs 和 BRBs 的详细信息，请参阅 [生成和发送 BRB](building-and-sending-a-brb.md)。

