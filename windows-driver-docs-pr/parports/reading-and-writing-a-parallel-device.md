---
title: 向并行设备进行读取和写入
description: 向并行设备进行读取和写入
ms.assetid: f28506b1-fa87-4119-a57a-2b49573197d8
keywords:
- 并行设备 WDK，读取
- 并行设备 WDK，写入
- 正在读取并行设备
- 编写并行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bfb5fb9e9c5f55097c1ea0f66b299eb6b8e3347
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845055"
---
# <a name="reading-and-writing-a-parallel-device"></a>向并行设备进行读取和写入





客户端通过使用[**IRP\_mj**](https://docs.microsoft.com/previous-versions/ff544164(v=vs.85))读取并写入并行设备，\_读取和[**IRP\_MJ\_写入**](https://docs.microsoft.com/previous-versions/ff544175(v=vs.85))请求。 内核模式驱动程序还可以使用系统提供的[**PPARALLEL\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_read)和[**PPARALLEL\_写入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_write)回调例程。 若要获取指向系统提供的读取和写入回调的指针，内核模式驱动程序使用[**IOCTL\_内部\_PARCLASS\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parclass_connect)请求，这将返回[**PARCLASS\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ns-parallel-_parclass_information)结构。 PARCLASS\_信息结构的**ParallelRead**和**ParallelWrite**成员是指向回调的指针。

如果客户端使用读取和写入 i/o 请求，则并行端口总线驱动程序会将并行设备工作队列上的请求排队。 在读取和写入设备之前，并行设备的客户端不必锁定并行端口，因为系统提供的用于并行端口的总线驱动程序会自动锁定并解锁客户端的端口。

 

 




