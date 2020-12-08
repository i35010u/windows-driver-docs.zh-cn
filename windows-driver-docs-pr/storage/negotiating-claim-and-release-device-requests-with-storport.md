---
title: 通过 Storport 协商声明和释放设备请求
description: 通过 Storport 协商声明和释放设备请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4efe1c2f6402f3aef5cf2bdc15ae658a4739b40f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804409"
---
# <a name="negotiating-claim-and-release-device-requests-with-storport"></a>通过 Storport 协商声明和释放设备请求


存储类驱动程序必须从 Storport 请求权限以 *声明* 设备。 有关类驱动程序如何声明设备的详细信息，请参阅 [存储类驱动程序的 ClaimDevice 例程](storage-class-driver-s-claimdevice-routine.md)。

根据设备是 PnP 设备还是预 PnP 存储设备，发现新设备并对其进行枚举的过程会有所不同。 Storport 驱动程序在尝试控制同一设备的预 PNP 和 PnP 驱动程序之间进行调节。 因此，存储设备驱动程序必须先从 Storport 获取权限，然后才能与其设备交互。 而且，所涉及的设备可能是 HBA 本身，也可能是连接到由 HBA 控制的目标的 LUN。 但是，当引用存储类驱动程序所声称的设备时，它始终是被声称的 LUN，而非 HBA。

若要获取使用设备的权限，则设备驱动程序将向 Storport 发送声明请求。 声明请求包含一个 IRP，其中的一个 IRP 具有 IOCTL SCSI 的 i/o 控制 \_ 代码 \_ \_ ，无执行无，以及一个指向 SRB 的指针。 **SRB**。 SRB 是函数类型 SRB \_ 函数 \_ 声明 \_ 设备。

Storport 为每个设备维护一个标志，用于指示设备是否已被占用。 Storport 将此标志设置为响应 SRB \_ 函数 \_ 声明 \_ 设备请求;Storport 清除标志以响应 SRB \_ 函数 \_ 删除 \_ 设备请求。

如果较高级别的驱动程序尝试声明不存在的设备，则 Storport 将无法进行声明请求 IRP，并返回状态 "设备不 \_ 存在" 状态 \_ \_ \_ 。

如果较高级别的驱动程序尝试声明一个已被声称的设备，则 Storport 将无法进行声明请求 IRP 并返回状态 \_ 设备繁忙状态 \_ 。

如果声明请求成功，则为 SRB 的数据缓冲区指针中的设备返回当前设备对象。

若要释放以前声明的设备，更高级别的驱动程序必须将 release 设备请求发送到 Storport 驱动程序： release 设备请求包含 **函数** 值为 SRB \_ 函数 \_ release 设备的 SRB \_ 。

有关从存储类驱动程序的角度来看的理赔设备请求的讨论，请参阅 [存储类驱动程序的 ClaimDevice 例程](storage-class-driver-s-claimdevice-routine.md)。

 

 




