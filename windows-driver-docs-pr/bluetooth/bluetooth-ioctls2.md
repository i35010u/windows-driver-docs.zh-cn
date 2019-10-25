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
ms.openlocfilehash: 8668dc295be7ea1470fc9da78d5e3176dce9986d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832137"
---
# <a name="bluetooth-ioctls"></a>蓝牙 IOCTL


蓝牙驱动程序堆栈提供具有多个 IOCTLs 的配置文件驱动程序，以收集以下相关信息：

-   本地蓝牙无线电和系统。

-   远程蓝牙设备。

-   导致即插即用（PnP）管理器加载配置文件驱动程序的设备。

若要收集有关本地蓝牙收音机和 system 的信息，配置文件驱动程序使用[**IOCTL\_BTH\_获取\_本地\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_local_info)。 IOCTL 返回后，其**AssociatedIrp SystemBuffer**成员包含指向[**BTH\_本地\_收音机\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ns-bthioctl-_bth_local_radio_info)结构的指针，其中包含有关本地蓝牙无线电和系统的信息，包括指示是否可以发现本地收音机并连接到。 返回的 BTH\_本地\_收音机\_信息结构包含一个[BTH\_设备\_info](https://go.microsoft.com/fwlink/p/?linkid=50713)结构，其中包含系统特定的信息，以及一个[**BTH\_收音机\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ns-bthioctl-_bth_radio_info)结构，这种结构包含特定于广播的本地信息。

若要收集有关特定远程蓝牙设备的信息，配置文件驱动程序使用[**IOCTL\_BTH\_获取\_无线电\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_radio_info)。 IOCTL 返回后，其**AssociatedIrp**将包含一个指向 BTH\_收音机\_INFO 结构的指针，该指针提供有关特定远程收音机的信息，包括是否可以发现远程收音机和连接到。

若要收集有关已发现的所有远程无线电的信息，配置文件驱动程序使用[**IOCTL\_BTH\_获取\_设备\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_device_info)。 IOCTL 返回后，它的**AssociatedIrp SystemBuffer**成员包含指向[**BTH\_设备的指针\_信息\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ns-bthioctl-_bth_device_info_list)结构，该结构包含 BTH\_设备\_INFO 结构的数组。 对于每个发现的远程广播，BTH\_设备\_信息\_列表结构包含一个数组项。 用户模式[BluetoothGetDeviceInfo](https://go.microsoft.com/fwlink/p/?linkid=74493) API 使用此功能返回有关所有远程无线电收发器的信息。

若要收集导致 PnP 管理器加载它的远程设备的相关信息，配置文件驱动程序使用[**IOCTL\_内部\_BTHENUM\_获取\_lnk-devinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_devinfo)。 IOCTL 返回后，其**AssociatedIrp**将包含一个指向 BTH\_设备的指针\_INFO 结构，其中包含有关远程设备的信息，包括其蓝牙设备地址、设备状态以及设备类（货货）设置。

配置文件驱动程序使用[**IOCTL\_内部\_BTHENUM\_获取\_ENUMINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_enuminfo) ，以获取导致 PnP 管理器加载配置文件驱动程序的底层设备和服务的相关信息。 IOCTL 返回后，其**AssociatedIrp**将包含一个指向[**BTH\_枚举器的指针\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_bth_enumerator_info)结构，其中包含供应商提供的有关设备的信息，包括端口号、设备标志、供应商 ID 和产品 ID。

有关使用蓝牙 IOCTLs 和 BRBs 的详细信息，请参阅[生成和发送 BRB](building-and-sending-a-brb.md)。

 

 





