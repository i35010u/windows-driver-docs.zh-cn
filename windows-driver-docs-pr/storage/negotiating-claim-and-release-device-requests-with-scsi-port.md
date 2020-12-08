---
title: 通过 SCSI 端口协商声明和释放设备请求
description: 通过 SCSI 端口协商声明和释放设备请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8d734292f643e61fdaae7db9889b920cd0ee7e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804415"
---
# <a name="negotiating-claim-and-release-device-requests-with-scsi-port"></a>通过 SCSI 端口协商声明和释放设备请求


## <span id="ddk_negotiating_claim_and_release_device_requests_with_scsi_port_kg"></span><span id="DDK_NEGOTIATING_CLAIM_AND_RELEASE_DEVICE_REQUESTS_WITH_SCSI_PORT_KG"></span>


存储类驱动程序必须请求 SCSI 端口的权限才能 *声明* 设备。 有关类驱动程序如何声明设备的详细信息，请参阅 [存储类驱动程序的 ClaimDevice 例程](storage-class-driver-s-claimdevice-routine.md)。

根据设备是 PnP 设备还是预 PnP 存储设备，发现新设备并对其进行枚举的过程会有所不同。 SCSI 端口驱动程序在尝试控制同一设备的预 PNP 和 PnP 驱动程序之间进行调节。 因此，存储设备驱动程序必须先从 SCSI 端口获取权限，然后才能与其设备交互。

若要获取使用设备的权限，则设备驱动程序会将声明请求发送到 SCSI 端口，通常在其 *AddDevice* 例程中。 声明请求包含一个 IRP，其中的一个 IRP 具有 IOCTL SCSI 的 i/o 控制 \_ 代码 \_ \_ ，无执行无，以及一个指向 SRB 的指针。 **SRB**。 SRB 是函数类型 SRB \_ 函数 \_ 声明 \_ 设备。

SCSI 端口会为每个设备维护一个标志，用于指示设备是否已被占用。 SCSI 端口会设置此标志，以响应 SRB \_ 函数 \_ 声明 \_ 设备请求;SCSI 端口会清除标志，以响应 SRB \_ 函数 \_ 删除 \_ 设备请求。

如果较高级别的驱动程序尝试声明不存在的设备，则 SCSI 端口将失败，声明请求 IRP 并返回状态 "设备不存在" 状态 \_ \_ \_ \_ 。

如果较高级别的驱动程序尝试声明已被声称的设备，则 SCSI 端口将失败，并且返回状态 \_ 设备 \_ 繁忙状态。

如果声明请求成功，则 SCSI 端口将在 SRB 的数据缓冲区指针中返回设备的当前设备对象。

若要释放以前声明的设备，更高级别的驱动程序必须将 release 设备请求发送到 SCSI 端口驱动程序： release 设备请求包含 **函数** 值为 SRB \_ 函数 \_ release 设备的 SRB \_ 。

有关从存储类驱动程序的角度来看的理赔设备请求的讨论，请参阅 [存储类驱动程序的 ClaimDevice 例程](storage-class-driver-s-claimdevice-routine.md)。

 

 




