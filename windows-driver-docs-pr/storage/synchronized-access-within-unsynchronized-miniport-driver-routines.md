---
title: 微型端口驱动程序例程中的同步的访问
description: 即使微型端口驱动程序在全双工模式下执行，或包含未同步的 Srb 处理，它可能仍需要同步的访问。
ms.assetid: a1bc3bff-b109-4a52-8466-48a0be7611b7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4226c5e572f252f5facc095e8150f50d46c6411b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390216"
---
# <a name="synchronized-access-within-miniport-driver-routines"></a>微型端口驱动程序例程中的同步的访问


## <span id="ddk_synchronized_access_within_unsynchronized_miniport_driver_routines"></span><span id="DDK_SYNCHRONIZED_ACCESS_WITHIN_UNSYNCHRONIZED_MINIPORT_DRIVER_ROUTINES"></span>


即使微型端口驱动程序在全双工模式下执行或执行 Srb 中的未同步的处理[ **HwStorBuildIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557369)例程，它可能仍需要同步的访问其设备扩展。 Storport 驱动程序提供的支持例程的库包括[ **StorPortSynchronizeAccess**](https://msdn.microsoft.com/library/windows/hardware/ff567511)，允许对关键数据的访问进行同步的微型端口驱动程序的例程结构等与设备的扩展。

当微型端口驱动程序调用**StorPortSynchronizeAccess**，它必须提供具有指向回调例程的例程。 回调例程包含必须与主机总线适配器的中断处理程序同步的 SRB 的处理的一部分。 为了提高性能，编写您的驱动程序可能执行的回调例程作为时间。

 

 




