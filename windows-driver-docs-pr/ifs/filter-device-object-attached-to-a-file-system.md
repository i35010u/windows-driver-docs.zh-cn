---
title: 附加到文件系统的筛选器设备对象
description: 附加到文件系统的筛选器设备对象
keywords:
- 筛选设备对象 WDK 文件系统
- 设备对象 i/o 请求 WDK 文件系统
- 筛选器驱动程序 WDK 文件系统，设备对象 i/o 请求
- 文件系统筛选器驱动程序 WDK，设备对象 i/o 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efabaa6f9cdb5af9ecc22596190080a91bde2228
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836483"
---
# <a name="filter-device-object-attached-to-a-file-system"></a>附加到文件系统的筛选器设备对象


## <span id="ddk_a_filter_device_object_attached_to_a_file_system_if"></span><span id="DDK_A_FILTER_DEVICE_OBJECT_ATTACHED_TO_A_FILE_SYSTEM_IF"></span>


若要筛选整个文件系统，文件系统筛选器驱动程序将创建一个筛选器设备对象，并将其附加到 "全局文件系统" 队列中的文件系统驱动程序 CDO 之上。

### <a name="span-idtypes_of_i_o_requests_that_are_sent_to_a_file_systemspanspan-idtypes_of_i_o_requests_that_are_sent_to_a_file_systemspantypes-of-io-requests-that-are-sent-to-a-file-system"></a><span id="types_of_i_o_requests_that_are_sent_to_a_file_system"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_A_FILE_SYSTEM"></span>发送到文件系统的 i/o 请求的类型

附加到文件系统上的筛选器设备对象通常会接收以下类型的 i/o 请求：

[**IRP \_ MJ \_ 设备 \_ 控制**](./irp-mj-device-control.md)

[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](./irp-mj-file-system-control.md)

[**IRP \_ MJ \_ 关闭**](./irp-mj-shutdown.md)

如果文件系统支持打开其控制设备对象的句柄，则筛选器也可能会看到以下类型的 i/o 请求：

[**IRP \_ MJ \_ 清除**](./irp-mj-cleanup.md)

[**IRP \_ MJ \_ 关闭**](./irp-mj-close.md)

[**IRP \_ MJ \_ 创建**](./irp-mj-create.md)

默认情况下，附加到文件系统的文件系统筛选器设备对象需要将所有无法识别或不需要的 Irp 传递到驱动程序堆栈上的下一个较低版本的驱动程序。

 

