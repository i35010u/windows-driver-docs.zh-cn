---
title: 在 KMDF 驱动程序中创建可分页的代码
description: 在 KMDF 驱动程序中创建可分页的代码
ms.assetid: 5c694ae2-2a16-4c2f-84b0-62e26f4121bc
keywords:
- 可分页驱动程序 WDK KMDF
- KMDF WDK，可分页驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a6e9963e90ab4957aac6698949c6c8d21f594ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844678"
---
# <a name="creating-pageable-code-in-a-kmdf-driver"></a>在 KMDF 驱动程序中创建可分页的代码


可*分页代码*是代码未使用时可以写入计算机的分页文件中的代码。 可以进行部分驱动程序分页以减少其负载映像和初始加载时间，还可以减少使用计算机的非分页内存池的驱动程序代码量。

若要帮助你确定可分页代码或数据是否适合你的驱动程序，请执行以下操作：

1.  标识驱动程序中的可分页部分。

    可分页节在需要之前不会加载到内存中。 有关如何在驱动程序中创建可分页的部分的信息，请参阅[使驱动程序可分页](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-drivers-pageable)。

2.  请确保分页的驱动程序代码不会妨碍计算机迅速从低功耗状态唤醒。

    驱动程序提供的所有设备对象回调函数都是在 IRQL = 被动\_级别调用的，这使你可以使其代码可分页（如[使驱动程序可分页](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-drivers-pageable)中所述）。

    但是，如果框架在设备处于低功耗状态时调用回调函数并返回到其工作（D0）状态，则不应使回调函数的代码可分页。

    如果此类代码是可分页的，则可能会在计算机进入睡眠状态之前将代码写入页面文件。 因此，计算机速度会变慢，因为无法重新加载您的代码（因而您的设备不能完全操作），直到寻呼磁盘的电源恢复。

    因此，在设备中列出的回调函数将[返回其工作状态](a-device-returns-to-its-working-state.md)主题。

3.  确定驱动程序是否需要访问驱动程序外部的可分页数据（如文件、注册表或页面缓冲池），然后再进行电源转换。

    有关如何启用和禁用驱动程序在电源转换期间访问可分页数据的功能的信息，请参阅[**WdfDeviceInitSetPowerPageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable)和[**WdfDeviceInitSetPowerNotPageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowernotpageable)。

    有关如何确定驱动程序处于不可分页状态的信息，请参阅[**WdfDevStateIsNP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevstateisnp)。

 

 





