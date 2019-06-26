---
title: 发送由内核模式驱动程序的 HID 报告
description: 发送由内核模式驱动程序的 HID 报告
ms.assetid: ff3d090f-cf76-40a7-9215-8440a592f303
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0c60a43259e99fe597b8f23cd4df57aff73ecb6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385804"
---
# <a name="sending-hid-reports-by-kernel-mode-drivers"></a>发送由内核模式驱动程序的 HID 报告


内核模式驱动程序应使用[ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)持续将输出报告发送到 HID 集合作为其主要的方法的请求。 驱动程序还可以使用 IOCTL\_HID\_设置\_*Xxx*发送输出报告和功能报表复制到集合的请求。 但是，驱动程序只应使用这些 I/O 请求设置集合的当前状态。 某些设备可能不支持[ **IOCTL\_HID\_设置\_输出\_报表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidclass/ni-hidclass-ioctl_hid_set_output_report)且会变得无响应，如果使用此请求。

有关详细信息，请参阅[使用 IRP\_MJ\_写入请求](#using-irp-mj-write-requests)并[使用 IOCTL\_HID\_设置\_Xxx 请求](#using-ioctl-hid-set-xxx-requests)。

### <a href="" id="using-irp-mj-write-requests"></a>使用 IRP\_MJ\_写入请求

Windows 2000 非 WDM 驱动程序和 Windows XP 和更高版本，驱动程序可以使用单个 IRP 发送到集合的所有写入请求。 但是，Windows 2000 WDM 驱动程序必须为每个写入请求分配新 IRP。 有关如何使用和重复使用 Irp 的详细信息，请参阅[处理 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)并[重用 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/reusing-irps)。

如果该驱动程序会写入 IRP，IRP 的重用[ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程应完成状态的状态请求\_详细\_处理\_必需 (不提供免费和 IRP）。 当驱动程序不再需要 IRP 时，应完成并释放通过调用 IRP [ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)并[ **IoFreeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)。 例如，驱动程序可能通常完成并释放 IRP 中的其[ **Unload** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程，或设备之后被删除。

如果驱动程序使用 IRP 为只有一个写请求，IRP [ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程应完成并释放 IRP，并返回状态\_成功。

在发送前输出报告，驱动程序必须首先初始化并设置输出报表缓冲区，如中所述[初始化 HID 报表](initializing-hid-reports.md)。 然后，该驱动程序必须使用 MDL 映射写入请求的输出报表缓冲区。 驱动程序调用[ **IoAllocateMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatemdl)若要为输出报告，并设置写入 IRP 分配 MDL **Irp-&gt;MdlAddress**成员添加到的 MDL 地址输出报表缓冲区。 当不再需要时，驱动程序必须释放报表缓冲区和 MDL。

除了设置写入 IRP MDL 地址，该驱动程序还必须设置下一步的较低级驱动程序的 I/O 堆栈位置。 驱动程序将通过调用获取 I/O 堆栈位置中的下一步的较低级驱动程序的访问权限[ **IoGetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation)。 该驱动程序设置的 I/O 堆栈位置的以下成员：

<a href="" id="parameters-write-length"></a>**Parameters.Write.Length**  
将设置为输出报告的长度，以字节为单位。 这应设置为 HID 集合的输出报表，由指定的长度**OutputReportByteLength**的集合的成员[ **HIDP\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_caps)结构。

<a href="" id="parameters-write-key"></a>**Parameters.Write.Key**  
设置为零。

<a href="" id="parameters-write-byteoffset-quadpart"></a>**Parameters.Write.ByteOffset.QuadPart**  
设置为零。

<a href="" id="majorfunction"></a>**MajorFunction**  
设置为 IRP\_MJ\_编写。

<a href="" id="fileobject"></a>**FileObject**  
将设置为表示 HID 集合上打开的文件的文件对象指针。

### <a href="" id="using-ioctl-hid-set-xxx-requests"></a>使用 IOCTL\_HID\_设置\_Xxx 请求

驱动程序还可以使用以下的 I/O 请求发送输出和到 HID 集合报告功能：

<a href="" id="ioctl-hid-set-output-report"></a>[**IOCTL\_HID\_设置\_输出\_报表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidclass/ni-hidclass-ioctl_hid_set_output_report)  
将输出报告发送到 （Windows XP 和更高版本） 的集合。

<a href="" id="ioctl-hid-set-feature"></a>[**IOCTL\_HID\_设置\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidclass/ni-hidclass-ioctl_hid_set_feature)  
将功能报表发送到的集合。

 

 




