---
title: 蓝牙 IOCTL
description: 蓝牙 IOCTL
ms.assetid: 384ea4bb-863c-4da7-bf81-85d2de734ef7
keywords:
- 蓝牙 WDK，IOCTLs
- IOCTLs WDK 蓝牙
- 本地蓝牙 WDK
- 远程蓝牙 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34f14d092e0fb1dde62491ed552978b29f10cc71
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733447"
---
# <a name="bluetooth-ioctls"></a>蓝牙 IOCTL


蓝牙驱动程序堆栈提供具有多个 IOCTLs 的配置文件驱动程序，以收集以下相关信息：

-   本地蓝牙无线电和系统。

-   远程蓝牙设备。

-   导致即插即用 (PnP) 管理器加载配置文件驱动程序的设备。

若要收集有关本地蓝牙收音机和 system 的信息，配置文件驱动程序使用 [**IOCTL \_ BTH \_ 获取 \_ 本地 \_ 信息**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_local_info)。 IOCTL 返回后，其 **AssociatedIrp.Sys的 temBuffer** 成员包含一个指向 [**BTH \_ 本地 \_ 无线电 \_ 信息**](/windows-hardware/drivers/ddi/bthioctl/ns-bthioctl-_bth_local_radio_info) 结构的指针，该结构包含有关本地蓝牙无线电和系统的信息，其中包括指示是否可以发现本地收音机并连接到的标志。 返回的 BTH \_ 本地 \_ 无线电 \_ 信息结构包含一个 [BTH \_ 设备 \_ 信息](/windows/win32/api/bthdef/ns-bthdef-bth_device_info) 结构，该结构包含系统特定的信息，以及一个 [**BTH \_ 无线 \_ 信息**](/windows-hardware/drivers/ddi/bthioctl/ns-bthioctl-_bth_radio_info) 结构，其中包含特定于无线电的特定信息。

若要收集有关特定远程蓝牙设备的信息，配置文件驱动程序将使用 [**IOCTL \_ BTH \_ 获取 \_ 无线电 \_ 信息**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_radio_info)。 IOCTL 返回后，其 **AssociatedIrp.Sys的 temBuffer** 成员包含一个指向 BTH 广播信息结构的指针， \_ \_ 该结构提供有关特定远程收音机的信息，包括是否可以发现远程收音机并连接到。

若要收集有关已发现的所有远程无线电的信息，配置文件驱动程序将使用 [**IOCTL \_ BTH \_ 获取 \_ 设备 \_ 信息**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_device_info)。 IOCTL 返回后，其 **AssociatedIrp.Sys的 temBuffer** 成员包含指向 [**BTH \_ 设备 \_ 信息 \_ 列表**](/windows-hardware/drivers/ddi/bthioctl/ns-bthioctl-_bth_device_info_list) 结构的指针，该结构包含 BTH \_ 设备 \_ 信息结构的数组。 BTH \_ 设备 \_ 信息 \_ 列表结构包含每个发现的远程广播的一个数组项。 用户模式 [BluetoothGetDeviceInfo](/windows/win32/api/bluetoothapis/nf-bluetoothapis-bluetoothgetdeviceinfo) API 使用此功能返回有关所有远程无线电收发器的信息。

若要收集导致 PnP 管理器加载它的远程设备的相关信息，配置文件驱动程序使用 [**IOCTL \_ INTERNAL \_ BTHENUM \_ GET \_ lnk-devinfo**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_devinfo)。 IOCTL 返回后，其 **AssociatedIrp.Sys的 temBuffer** 成员包含一个指向 BTH \_ 设备 \_ 信息结构的指针，该结构包含有关远程设备的信息，其中包括该远程设备的蓝牙设备地址、设备状态以及设备 (货到) 设置。

配置文件驱动程序使用 [**IOCTL \_ INTERNAL \_ BTHENUM \_ GET \_ ENUMINFO**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_enuminfo) 获取有关导致 PnP 管理器加载配置文件驱动程序的底层设备和服务的信息。 IOCTL 返回后，其 **AssociatedIrp.Sys的 temBuffer** 成员包含指向 [**BTH \_ 枚举器 \_ 信息**](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_bth_enumerator_info) 结构的指针，该结构包含有关设备的供应商提供的信息，其中包括端口号、设备标志、供应商 id 和产品 ID。

有关使用蓝牙 IOCTLs 和 BRBs 的详细信息，请参阅 [生成和发送 BRB](building-and-sending-a-brb.md)。

