---
title: 微型端口驱动程序例程内的同步访问
description: 即使微型端口驱动程序在全双工模式下执行或 SRBs 处理未同步，它仍可能需要同步访问。
ms.assetid: a1bc3bff-b109-4a52-8466-48a0be7611b7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ee0f723f270112655b821948ddc9c7529b77942
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844451"
---
# <a name="synchronized-access-within-miniport-driver-routines"></a>微型端口驱动程序例程内的同步访问


## <span id="ddk_synchronized_access_within_unsynchronized_miniport_driver_routines"></span><span id="DDK_SYNCHRONIZED_ACCESS_WITHIN_UNSYNCHRONIZED_MINIPORT_DRIVER_ROUTINES"></span>


即使微型端口驱动程序在全双工模式下执行，或者在[**HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio)例程中进行 SRBs 的不同步处理，它仍可能需要同步访问其设备扩展。 Storport 驱动程序提供的支持例程库包括[**StorPortSynchronizeAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportsynchronizeaccess)，后者允许微型端口驱动程序同步对关键数据结构（如设备扩展）的访问。

当微型端口驱动程序调用**StorPortSynchronizeAccess**时，它必须提供指向回调例程的指针。 回调例程包含必须与主机总线适配器的中断处理程序同步的 SRB 处理部分。 为了获得更好的性能，请编写你的驱动程序，使其尽可能少地执行回调例程。

 

 




