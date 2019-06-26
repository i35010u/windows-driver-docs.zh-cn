---
title: 微型端口驱动程序例程中的同步的访问
description: 即使微型端口驱动程序在全双工模式下执行，或包含未同步的 Srb 处理，它可能仍需要同步的访问。
ms.assetid: a1bc3bff-b109-4a52-8466-48a0be7611b7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36356b9dc397d6bdff826a76e4d6e483f3c6a348
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368163"
---
# <a name="synchronized-access-within-miniport-driver-routines"></a>微型端口驱动程序例程中的同步的访问


## <span id="ddk_synchronized_access_within_unsynchronized_miniport_driver_routines"></span><span id="DDK_SYNCHRONIZED_ACCESS_WITHIN_UNSYNCHRONIZED_MINIPORT_DRIVER_ROUTINES"></span>


即使微型端口驱动程序在全双工模式下执行或执行 Srb 中的未同步的处理[ **HwStorBuildIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_buildio)例程，它可能仍需要同步的访问其设备扩展。 Storport 驱动程序提供的支持例程的库包括[ **StorPortSynchronizeAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportsynchronizeaccess)，允许对关键数据的访问进行同步的微型端口驱动程序的例程结构等与设备的扩展。

当微型端口驱动程序调用**StorPortSynchronizeAccess**，它必须提供具有指向回调例程的例程。 回调例程包含必须与主机总线适配器的中断处理程序同步的 SRB 的处理的一部分。 为了提高性能，编写您的驱动程序可能执行的回调例程作为时间。

 

 




