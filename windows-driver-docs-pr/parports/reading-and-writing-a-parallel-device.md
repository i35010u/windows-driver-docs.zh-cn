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
ms.openlocfilehash: 99269ba715b430b099d5e1a8f556ed9c5fdcd668
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384739"
---
# <a name="reading-and-writing-a-parallel-device"></a>向并行设备进行读取和写入





客户端通过使用 [**IRP \_ mj \_ READ**](/previous-versions/ff544164(v=vs.85)) 和 [**irp \_ mj \_ 写入**](/previous-versions/ff544175(v=vs.85)) 请求来读取和写入并行设备。 内核模式驱动程序还可以使用系统提供的 [**PPARALLEL \_ READ**](/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_read) 和 [**PPARALLEL \_ 写入**](/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_write) 回调例程。 若要获取指向系统提供的读取和写入回调的指针，内核模式驱动程序使用 [**IOCTL \_ 内部 \_ PARCLASS \_ CONNECT**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parclass_connect) 请求，该请求将返回 [**PARCLASS \_ 信息**](/windows-hardware/drivers/ddi/parallel/ns-parallel-_parclass_information) 结构。 PARCLASS 信息结构的 **ParallelRead** 和 **ParallelWrite** 成员 \_ 是指向回调的指针。

如果客户端使用读取和写入 i/o 请求，则并行端口总线驱动程序会将并行设备工作队列上的请求排队。 在读取和写入设备之前，并行设备的客户端不必锁定并行端口，因为系统提供的用于并行端口的总线驱动程序会自动锁定并解锁客户端的端口。

 

