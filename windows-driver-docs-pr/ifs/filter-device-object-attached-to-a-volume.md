---
title: 附加到卷的筛选器设备对象
description: 附加到卷的筛选器设备对象
keywords:
- 筛选设备对象 WDK 文件系统
- 筛选器驱动程序 WDK 文件系统，设备对象 i/o 请求
- 文件系统筛选器驱动程序 WDK，设备对象 i/o 请求
- 卷 WDK 文件系统，设备对象 i/o 请求
- 设备对象 i/o 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d5333de1f460a77098e0b72f6bd8747d1ac1a31
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836481"
---
# <a name="filter-device-object-attached-to-a-volume"></a>附加到卷的筛选器设备对象


## <span id="ddk_a_filter_device_object_attached_to_a_volume_if"></span><span id="DDK_A_FILTER_DEVICE_OBJECT_ATTACHED_TO_A_VOLUME_IF"></span>


若要筛选卷，筛选器驱动程序将创建一个筛选器设备对象，并将其附加到该卷的卷设备对象上。

### <a name="span-idtypes_of_i_o_requests_that_are_sent_to_a_volumespanspan-idtypes_of_i_o_requests_that_are_sent_to_a_volumespantypes-of-io-requests-that-are-sent-to-a-volume"></a><span id="types_of_i_o_requests_that_are_sent_to_a_volume"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_A_VOLUME"></span>发送到卷的 i/o 请求的类型

附加到卷上方的筛选器设备对象通常会收到以下类型的 i/o 请求：

[**IRP \_ MJ \_ 清除**](./irp-mj-cleanup.md)

[**IRP \_ MJ \_ 关闭**](./irp-mj-close.md)

[**IRP \_ MJ \_ 创建**](./irp-mj-create.md)

[**IRP \_ MJ \_ 设备 \_ 控制**](./irp-mj-device-control.md)

[**IRP \_ MJ \_ 目录 \_ 控件**](./irp-mj-directory-control.md)

[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](./irp-mj-file-system-control.md)

[**IRP \_ MJ \_ 刷新 \_ 缓冲区**](./irp-mj-flush-buffers.md)

[**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md)

[**IRP \_ MJ \_ 锁定 \_ 控制**](./irp-mj-lock-control.md)

[**IRP \_ MJ \_ PNP**](./irp-mj-pnp.md)

[**IRP \_ MJ \_ 查询 \_ EA**](./irp-mj-query-ea.md)

[**IRP \_ MJ \_ 查询 \_ 信息**](./irp-mj-query-information.md)

[**IRP \_ MJ \_ 查询 \_ 配额**](./irp-mj-query-quota.md)

[**IRP \_ MJ \_ 查询 \_ 安全性**](./irp-mj-query-security.md)

[**IRP \_ MJ \_ 查询 \_ 卷 \_ 信息**](./irp-mj-query-volume-information.md)

[**IRP \_ MJ \_ 读取**](./irp-mj-read.md)

[**IRP \_ MJ \_ 设置 \_ EA**](./irp-mj-set-ea.md)

[**IRP \_ MJ \_ 设置 \_ 信息**](./irp-mj-set-information.md)

[**IRP \_ MJ \_ 设置 \_ 配额**](./irp-mj-set-quota.md)

[**IRP \_ MJ \_ 设置 \_ 安全性**](./irp-mj-set-security.md)

[**IRP \_ MJ \_ 设置 \_ 卷 \_ 信息**](./irp-mj-set-volume-information.md)

[**IRP \_ MJ \_ 关闭**](./irp-mj-shutdown.md)

[**IRP \_ MJ \_ 写入**](./irp-mj-write.md)

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

默认情况下，文件系统筛选器设备对象（附加到卷）需要将所有无法识别或不需要的 Irp 传递到驱动程序堆栈上的下一个较低版本的驱动程序。 此外，它们必须实现 **FastIoDetachDevice**。

**注意**   在 Microsoft Windows XP 和更高版本中，以下快速 i/o 回调例程已过时，不应由文件系统筛选器驱动程序使用： **AcquireForCcFlush**

**AcquireFileForNtCreateSection**

**AcquireForModWrite**

**ReleaseForCcFlush**

**ReleaseFileForNtCreateSection**

**ReleaseForModWrite**

有关详细信息，请参阅 [**FsRtlRegisterFileSystemFilterCallbacks**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)的参考条目。

 

 

