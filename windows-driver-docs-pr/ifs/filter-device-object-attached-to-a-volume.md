---
title: 附加到卷的筛选器设备对象
description: 附加到卷的筛选器设备对象
ms.assetid: cf152065-fc03-4f5f-b65b-13a76e83d745
keywords:
- 筛选设备对象 WDK 文件系统
- 筛选驱动程序 WDK 文件系统中，设备对象 I/O 请求
- 文件系统筛选器驱动程序 WDK，设备对象 I/O 请求
- WDK 卷文件系统、 设备对象 I/O 请求
- 设备对象 I/O 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e90725415de436bfec0c21f6f19ec61630c8c5d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369249"
---
# <a name="filter-device-object-attached-to-a-volume"></a>附加到卷的筛选器设备对象


## <span id="ddk_a_filter_device_object_attached_to_a_volume_if"></span><span id="DDK_A_FILTER_DEVICE_OBJECT_ATTACHED_TO_A_VOLUME_IF"></span>


若要筛选一个卷，筛选器驱动程序创建一个筛选器设备对象并将其附加卷的卷设备对象上方。

### <a name="span-idtypesofiorequeststhataresenttoavolumespanspan-idtypesofiorequeststhataresenttoavolumespantypes-of-io-requests-that-are-sent-to-a-volume"></a><span id="types_of_i_o_requests_that_are_sent_to_a_volume"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_A_VOLUME"></span>类型的 I/O 请求发送到的卷

附加卷上面的筛选器设备对象通常会收到以下类型的 I/O 请求：

[**IRP\_MJ\_CLEANUP**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-cleanup)

[**IRP\_MJ\_CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-close)

[**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)

[**IRP\_MJ\_DEVICE\_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-device-control)

[**IRP\_MJ\_DIRECTORY\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control)

[**IRP\_MJ\_文件\_系统\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)

[**IRP\_MJ\_刷新\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-flush-buffers)

[**IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-internal-device-control)

[**IRP\_MJ\_锁\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control)

[**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-pnp)

[**IRP\_MJ\_查询\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea)

[**IRP\_MJ\_查询\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-information)

[**IRP\_MJ\_查询\_配额**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota)

[**IRP\_MJ\_QUERY\_SECURITY**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security)

[**IRP\_MJ\_查询\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information)

[**IRP\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-read)

[**IRP\_MJ\_SET\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea)

[**IRP\_MJ\_SET\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-information)

[**IRP\_MJ\_SET\_QUOTA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota)

[**IRP\_MJ\_SET\_SECURITY**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security)

[**IRP\_MJ\_设置\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information)

[**IRP\_MJ\_SHUTDOWN**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-shutdown)

[**IRP\_MJ\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-write)

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

文件系统筛选器设备对象，附加的卷，需要默认情况下将所有无法识别或不需要的 Irp 传递给下一步低驱动程序，驱动程序堆栈上。 此外，它们必须实现**FastIoDetachDevice**。

**请注意**  上 Microsoft Windows XP 和更高版本，下面的快速 I/O 回调例程已过时，并且不能由文件系统筛选器驱动程序：**AcquireForCcFlush**

**AcquireFileForNtCreateSection**

**AcquireForModWrite**

**ReleaseForCcFlush**

**ReleaseFileForNtCreateSection**

**ReleaseForModWrite**

有关详细信息，请参阅引用条目[ **FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)。

 

 

 




