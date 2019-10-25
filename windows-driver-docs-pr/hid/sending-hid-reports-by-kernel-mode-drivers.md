---
title: 通过内核模式驱动程序发送 HID 报表
description: 通过内核模式驱动程序发送 HID 报表
ms.assetid: ff3d090f-cf76-40a7-9215-8440a592f303
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 266de90bb6b6505649c4a0c698492c5d023f60f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841559"
---
# <a name="sending-hid-reports-by-kernel-mode-drivers"></a>通过内核模式驱动程序发送 HID 报表


内核模式驱动程序应使用[**IRP\_MJ\_写入**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求，作为将输出连续发送到 HID 集合的主要方法。 驱动程序还可以使用 IOCTL\_HID\_设置\_*Xxx*请求，以将输出报告和功能报告发送到集合。 但是，驱动程序应仅使用这些 i/o 请求来设置集合的当前状态。 某些设备可能不支持[**IOCTL\_HID\_设置\_输出\_报告**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_set_output_report)，并将在使用此请求时停止响应。

有关详细信息，请参阅[使用 IRP\_MJ\_写入请求](#using-irp-mj-write-requests)和[使用 IOCTL\_HID\_设置\_Xxx 请求](#using-ioctl-hid-set-xxx-requests)。

### <a href="" id="using-irp-mj-write-requests"></a>使用 IRP\_MJ\_写入请求

对于适用于 Windows XP 及更高版本的非 WDM Windows 2000 驱动程序和驱动程序，可以对发送到集合的所有写入请求使用单个 IRP。 但是，Windows 2000 WDM 驱动程序必须为每个写入请求分配新的 IRP。 有关如何使用和重用 Irp 的详细信息，请参阅[处理 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)和[重用 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/reusing-irps)。

如果驱动程序重用写入 IRP，则 IRP 的[**IoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程应完成状态为 "状态\_更多\_\_处理的请求（而不是释放 IRP）。 当驱动程序不再需要 IRP 时，应通过调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)和[**IoFreeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)来完成并释放 irp。 例如，驱动程序通常可能在其[**卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程中完成并释放 IRP，或在删除设备之后。

如果驱动程序只对一个写入请求使用 IRP，则 IRP 的[**IoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程应完成并释放 irp，并返回状态\_SUCCESS。

在发送输出报告之前，驱动程序必须先初始化并设置输出报告缓冲区，如[初始化 HID 报告](initializing-hid-reports.md)中所述。 然后，该驱动程序必须使用 MDL 来映射写入请求的输出报告缓冲区。 驱动程序调用[**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)为输出报告分配 MDL，并将写入 Irp 的**irp&gt;MdlAddress**成员设置为输出报告缓冲区的 mdl 地址。 当不再需要报表缓冲区和 MDL 时，驱动程序必须将其释放。

除了设置写入 IRP 的 MDL 地址外，驱动程序还必须设置下一个较低级别驱动程序的 i/o 堆栈位置。 驱动程序通过调用[**IoGetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)获取对下一个较低级别驱动程序的 i/o 堆栈位置的访问。 驱动程序设置 i/o 堆栈位置的以下成员：

<a href="" id="parameters-write-length"></a>**Parameters。写入长度**  
设置为输出报表的长度（以字节为单位）。 此设置应设置为 HID 集合的输出报告的长度，由集合的[**HIDP\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps) **OutputReportByteLength**成员指定。

<a href="" id="parameters-write-key"></a>**Parameters。写入密钥**  
设置为零。

<a href="" id="parameters-write-byteoffset-quadpart"></a>**ByteOffset. QuadPart**  
设置为零。

<a href="" id="majorfunction"></a>**MajorFunction**  
设置为 IRP\_MJ\_写入。

<a href="" id="fileobject"></a>**FileObject**  
设置为表示 HID 集合上打开的文件的文件对象指针。

### <a href="" id="using-ioctl-hid-set-xxx-requests"></a>使用 IOCTL\_HID\_设置\_Xxx 请求

驱动程序还可以使用以下 i/o 请求将输出和功能报告发送到 HID 集合：

<a href="" id="ioctl-hid-set-output-report"></a>[ **\_HID\_设置\_输出\_报表的 IOCTL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_set_output_report)  
将输出报告发送到集合（Windows XP 及更高版本）。

<a href="" id="ioctl-hid-set-feature"></a>[**IOCTL\_HID\_设置\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_set_feature)  
向集合发送功能报表。

 

 




