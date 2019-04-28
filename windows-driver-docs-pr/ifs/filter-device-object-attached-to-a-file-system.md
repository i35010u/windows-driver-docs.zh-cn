---
title: 附加到文件系统的筛选器设备对象
description: 附加到文件系统的筛选器设备对象
ms.assetid: 5fb0ec43-a639-4b2a-8057-3313e9dee457
keywords:
- 筛选设备对象 WDK 文件系统
- 设备对象 I/O 请求 WDK 文件系统
- 筛选驱动程序 WDK 文件系统中，设备对象 I/O 请求
- 文件系统筛选器驱动程序 WDK，设备对象 I/O 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ac461c09b91c00ec11118f1cc0907d751e22227
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341519"
---
# <a name="filter-device-object-attached-to-a-file-system"></a>附加到文件系统的筛选器设备对象


## <span id="ddk_a_filter_device_object_attached_to_a_file_system_if"></span><span id="DDK_A_FILTER_DEVICE_OBJECT_ATTACHED_TO_A_FILE_SYSTEM_IF"></span>


若要筛选的整个文件系统，文件系统筛选器驱动程序创建一个筛选器设备对象，并将其附加在全局文件系统队列中的文件系统驱动程序的 CDO 上面。

### <a name="span-idtypesofiorequeststhataresenttoafilesystemspanspan-idtypesofiorequeststhataresenttoafilesystemspantypes-of-io-requests-that-are-sent-to-a-file-system"></a><span id="types_of_i_o_requests_that_are_sent_to_a_file_system"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_A_FILE_SYSTEM"></span>类型的 I/O 请求发送到文件系统

文件系统上附加的筛选器设备对象通常会收到以下类型的 I/O 请求：

[**IRP\_MJ\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff548649)

[**IRP\_MJ\_文件\_系统\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff548670)

[**IRP\_MJ\_SHUTDOWN**](https://msdn.microsoft.com/library/windows/hardware/ff549423)

如果文件系统支持对其控制设备对象的打开句柄，筛选器可能会看到以下类型的 I/O 的请求：

[**IRP\_MJ\_CLEANUP**](https://msdn.microsoft.com/library/windows/hardware/ff548608)

[**IRP\_MJ\_CLOSE**](https://msdn.microsoft.com/library/windows/hardware/ff548621)

[**IRP\_MJ\_CREATE**](https://msdn.microsoft.com/library/windows/hardware/ff548630)

文件系统筛选器设备对象附加到文件系统需要默认情况下将所有无法识别或不需要的 Irp 传递给下一步低驱动程序，驱动程序堆栈上。

 

 




