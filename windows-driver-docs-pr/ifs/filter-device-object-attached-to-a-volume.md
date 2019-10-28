---
title: 附加到卷的筛选器设备对象
description: 附加到卷的筛选器设备对象
ms.assetid: cf152065-fc03-4f5f-b65b-13a76e83d745
keywords:
- 筛选设备对象 WDK 文件系统
- 筛选器驱动程序 WDK 文件系统，设备对象 i/o 请求
- 文件系统筛选器驱动程序 WDK，设备对象 i/o 请求
- 卷 WDK 文件系统，设备对象 i/o 请求
- 设备对象 i/o 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db370e568d32fff6a1cd5b220557ee2e14ac3dac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841401"
---
# <a name="filter-device-object-attached-to-a-volume"></a>附加到卷的筛选器设备对象


## <span id="ddk_a_filter_device_object_attached_to_a_volume_if"></span><span id="DDK_A_FILTER_DEVICE_OBJECT_ATTACHED_TO_A_VOLUME_IF"></span>


若要筛选卷，筛选器驱动程序将创建一个筛选器设备对象，并将其附加到该卷的卷设备对象上。

### <a name="span-idtypes_of_i_o_requests_that_are_sent_to_a_volumespanspan-idtypes_of_i_o_requests_that_are_sent_to_a_volumespantypes-of-io-requests-that-are-sent-to-a-volume"></a><span id="types_of_i_o_requests_that_are_sent_to_a_volume"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_A_VOLUME"></span>发送到卷的 i/o 请求的类型

附加到卷上方的筛选器设备对象通常会收到以下类型的 i/o 请求：

[**IRP\_MJ\_清除**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-cleanup)

[**IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-close)

[**IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)

[**IRP\_MJ\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-device-control)

[**IRP\_MJ\_DIRECTORY\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control)

[**IRP\_MJ\_文件\_系统\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)

[**IRP\_MJ\_刷新\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-flush-buffers)

[**IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-internal-device-control)

[**IRP\_MJ\_锁定\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control)

[**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-pnp)

[**IRP\_MJ\_QUERY\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea)

[**IRP\_MJ\_查询\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-information)

[**IRP\_MJ\_QUERY\_配额**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota)

[**IRP\_MJ\_QUERY\_安全性**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security)

[**IRP\_MJ\_查询\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information)

[**IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-read)

[**IRP\_MJ\_集\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea)

[**IRP\_MJ\_集\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-information)

[**IRP\_MJ\_集\_配额**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota)

[**IRP\_MJ\_集\_安全性**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security)

[**IRP\_MJ\_设置\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information)

[**IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-shutdown)

[**IRP\_MJ\_写入**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-write)

**FastIoCheckIfPossible**

**FastIoDetachDevice**

**FastIoDeviceControl**

**FastIoLock**

**FastIoQueryBasicInfo**

**FastIoQueryNetworkOpenInfo**

**FastIoQueryOpen**

**FastIoQueryStandardInfo**

**FastIoRead**

**FastIoReadCompressed**

**FastIoUnlockAll**

**FastIoUnlockAllByKey**

**FastIoUnlockSingle**

**FastIoWrite**

**FastIoWriteCompressed**

**MdlRead**

**MdlReadComplete**

**MdlReadCompleteCompressed**

**MdlWriteComplete**

**MdlWriteCompleteCompressed**

**PrepareMdlWrite**

默认情况下，文件系统筛选器设备对象（附加到卷）需要将所有无法识别或不需要的 Irp 传递到驱动程序堆栈上的下一个较低版本的驱动程序。 此外，它们必须实现**FastIoDetachDevice**。

**注意**   在 MICROSOFT Windows XP 和更高版本上，以下快速 i/o 回调例程已过时，不应由文件系统筛选器驱动程序使用： **AcquireForCcFlush**

**AcquireFileForNtCreateSection**

**AcquireForModWrite**

**ReleaseForCcFlush**

**ReleaseFileForNtCreateSection**

**ReleaseForModWrite**

有关详细信息，请参阅[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)的参考条目。

 

 

 




