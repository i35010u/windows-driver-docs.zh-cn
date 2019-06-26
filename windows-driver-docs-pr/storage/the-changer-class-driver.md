---
title: 更换器类驱动程序
description: 更换器类驱动程序
ms.assetid: c1c2330c-9cfc-432f-945c-630dc16aa54d
keywords:
- 更换器驱动程序 WDK 存储类驱动程序
- 存储更换器驱动程序 WDK、 类驱动程序
- 类驱动程序 WDK 存储，更换器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a335cd9dec3c85127de78dee5c7f919a1df6315b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386806"
---
# <a name="the-changer-class-driver"></a>更换器类驱动程序


## <span id="ddk_the_changer_class_driver_kg"></span><span id="DDK_THE_CHANGER_CLASS_DRIVER_KG"></span>


转换器类驱动程序执行特定于操作系统的、 独立于设备的硬件供应商提供的转换器 miniclass 驱动程序服务。 有关转换器 miniclass 驱动程序的详细信息，请参阅[Vendor-Supplied 更换器驱动程序](vendor-supplied-changer-drivers.md)。

转换器类驱动程序：

-   提供了 miniclass 驱动程序调用来分配和释放的分配例程建立一个内存池的内存。

-   提供了将同步 Srb 发送到 Microsoft Windows XP 和更高版本操作系统中的端口驱动程序的一种独立于操作系统的方法 (请参阅[转换器类驱动程序版本差异](differences-in-changer-class-driver-versions.md)有关的说明Windows 2000 和 Windows XP 之间差异）。

-   可帮助进行初始化的类/miniclass 驱动程序对。

-   调用 **换带机 * * * Xxx* miniclass 驱动程序例程，以确定要为特定于设备的信息分配和准备换带机接收其他请求的空间量。

-   执行与设备无关的预处理[ **IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求时，调用相应 **换带机 * * * Xxx* miniclass 例程，并完成请求。

-   执行独立于设备的预处理错误并调用 miniclass 驱动[ **ChangerError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changererror)例程进行特定于设备的处理。

-   调用 **换带机 * * * Xxx* miniclass 驱动程序例程，以获取产品数据，更改元素的状态，或查询查询或批量标记数据。

 

 




