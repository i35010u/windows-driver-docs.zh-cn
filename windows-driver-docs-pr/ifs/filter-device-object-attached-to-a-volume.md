---
title: 筛选设备对象附加到的卷
description: 筛选设备对象附加到的卷
ms.assetid: cf152065-fc03-4f5f-b65b-13a76e83d745
keywords:
- 筛选设备对象 WDK 文件系统
- 筛选驱动程序 WDK 文件系统中，设备对象 I/O 请求
- 文件系统筛选器驱动程序 WDK，设备对象 I/O 请求
- WDK 卷文件系统、 设备对象 I/O 请求
- 设备对象 I/O 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85ee67d1928696ea0e49789e21259748af9ff07b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547383"
---
# <a name="filter-device-object-attached-to-a-volume"></a>筛选设备对象附加到的卷


## <span id="ddk_a_filter_device_object_attached_to_a_volume_if"></span><span id="DDK_A_FILTER_DEVICE_OBJECT_ATTACHED_TO_A_VOLUME_IF"></span>


若要筛选一个卷，筛选器驱动程序创建一个筛选器设备对象并将其附加卷的卷设备对象上方。

### <a name="span-idtypesofiorequeststhataresenttoavolumespanspan-idtypesofiorequeststhataresenttoavolumespantypes-of-io-requests-that-are-sent-to-a-volume"></a><span id="types_of_i_o_requests_that_are_sent_to_a_volume"></span><span id="TYPES_OF_I_O_REQUESTS_THAT_ARE_SENT_TO_A_VOLUME"></span>类型的 I/O 请求发送到的卷

附加卷上面的筛选器设备对象通常会收到以下类型的 I/O 请求：

[**IRP\_MJ\_CLEANUP**](https://msdn.microsoft.com/library/windows/hardware/ff548608)

[**IRP\_MJ\_CLOSE**](https://msdn.microsoft.com/library/windows/hardware/ff548621)

[**IRP\_MJ\_CREATE**](https://msdn.microsoft.com/library/windows/hardware/ff548630)

[**IRP\_MJ\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff548649)

[**IRP\_MJ\_DIRECTORY\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff548658)

[**IRP\_MJ\_文件\_系统\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff548670)

[**IRP\_MJ\_刷新\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff549235)

[**IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff549241)

[**IRP\_MJ\_锁\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff549251)

[**IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff549268)

[**IRP\_MJ\_查询\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549279)

[**IRP\_MJ\_查询\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff549283)

[**IRP\_MJ\_查询\_配额**](https://msdn.microsoft.com/library/windows/hardware/ff549293)

[**IRP\_MJ\_QUERY\_SECURITY**](https://msdn.microsoft.com/library/windows/hardware/ff549298)

[**IRP\_MJ\_查询\_卷\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff549318)

[**IRP\_MJ\_READ**](https://msdn.microsoft.com/library/windows/hardware/ff549327)

[**IRP\_MJ\_SET\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549346)

[**IRP\_MJ\_SET\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff549366)

[**IRP\_MJ\_SET\_QUOTA**](https://msdn.microsoft.com/library/windows/hardware/ff549401)

[**IRP\_MJ\_SET\_SECURITY**](https://msdn.microsoft.com/library/windows/hardware/ff549407)

[**IRP\_MJ\_设置\_卷\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff549415)

[**IRP\_MJ\_SHUTDOWN**](https://msdn.microsoft.com/library/windows/hardware/ff549423)

[**IRP\_MJ\_WRITE**](https://msdn.microsoft.com/library/windows/hardware/ff549427)

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

有关详细信息，请参阅引用条目[ **FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)。

 

 

 




