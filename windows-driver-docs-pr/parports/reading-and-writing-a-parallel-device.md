---
title: 向并行设备进行读取和写入
description: 向并行设备进行读取和写入
ms.assetid: f28506b1-fa87-4119-a57a-2b49573197d8
keywords:
- 并行设备 WDK，读取
- 并行设备 WDK、 写入
- 读取并行设备
- 编写并行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 955d2f5f346e48ef0ba12b1b3b5243c4da6084fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358492"
---
# <a name="reading-and-writing-a-parallel-device"></a>向并行设备进行读取和写入





客户端读取，并通过使用写入并行设备[ **IRP\_MJ\_读取**](https://docs.microsoft.com/previous-versions/ff544164(v=vs.85))并[ **IRP\_MJ\_写**](https://docs.microsoft.com/previous-versions/ff544175(v=vs.85))请求。 内核模式驱动程序还可以使用系统提供[ **PPARALLEL\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_read)并[ **PPARALLEL\_编写**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_write)回调例程。 若要获取指向系统提供的读取和编写回调，内核模式驱动程序将使用[ **IOCTL\_内部\_PARCLASS\_CONNECT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_parclass_connect)请求，它将返回[ **PARCLASS\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ns-parallel-_parclass_information)结构。 **ParallelRead**并**ParallelWrite** PARCLASS 成员\_信息结构都是指向回调。

如果使用读取和写入 I/O 请求的客户端，并行端口总线驱动程序将在工作队列的并行设备请求排队。 并行的设备的客户端不需要读取和写入设备，因为并行端口的系统提供的总线驱动程序进行自动锁定和解锁该端口的客户端之前锁定并行端口。

 

 




