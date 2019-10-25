---
title: 通过内核模式驱动程序获取 HID 报表
description: 本主题讨论内核模式驱动程序应如何使用 IRP_MJ_READ 请求作为连续获取 HID 输入报告的主要方法。
ms.assetid: 017481f1-8021-4fd5-ab8e-f09f6006e616
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ec133e6e0b0e67653339ae64e3e612f60e20f6d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841569"
---
# <a name="obtaining-hid-reports-by-kernel-mode-drivers"></a>通过内核模式驱动程序获取 HID 报表


本主题讨论内核模式驱动程序应如何使用[**IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)请求作为连续获取 HID 输入报告的主要方法。

连续读取请求按从集合接收输入报告的顺序返回输入报告。 驱动程序还可以使用 IOCTL\_HID\_获取\_*Xxx*请求以获取输入和功能报告。 但是，驱动程序应仅使用这些 i/o 请求来获取设备的当前状态。 如果驱动程序尝试使用 IOCTL\_HID\_获取\_输入\_报表以连续获取输入报表，则报表可能会丢失。 此外，某些设备可能不支持 IOCTL\_HID\_获取\_输入\_报告，并将在使用此请求时停止响应。

以下各节提供了详细信息。

### <a href="" id="using-irp-ml-read-requests"></a>使用 IRP\_MJ\_读取请求

对于 Windows XP 及更高版本的非 WDM Windows 2000 驱动程序和驱动程序，可以对设备使用单个 IRP 来处理所有读取请求。 但是，Windows 2000 WDM 驱动程序必须为每个读取请求分配新的 IRP。 有关如何使用和重用 Irp 的一般信息，请参阅[处理 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)和[重用 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/reusing-irps)。

如果驱动程序重用 IRP，则 IRP 的[**IoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程应完成状态为 "状态"\_更\_\_处理的请求（而不是使用 IRP）。 当驱动程序不再需要 IRP 时，应通过调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)和[**IoFreeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)来完成并释放 irp。 例如，驱动程序通常可能在其[*卸载*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程中完成并释放 IRP，或在删除设备之后。

如果驱动程序只对一个读取请求使用 IRP，则 IRP 的**IoCompletion**例程应完成并释放 irp，并返回状态\_SUCCESS。

在驱动程序可以请求输入报告之前，必须先从非分页内存池分配一个0初始化的输入报告缓冲区。 缓冲区的大小（以字节为单位）由 HID 集合的[**HIDP\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)结构的**InputReportByteLength**成员指定。 然后，驱动程序必须使用 MDL 来映射读取请求的输入报告缓冲区。 驱动程序调用[**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)为输入报告缓冲区分配 MDL，并将 read Irp 的**irp&gt;MdlAddress**成员设置为输入报告缓冲区的 mdl 地址。 当不再需要报表缓冲区和 MDL 时，驱动程序应释放它。

除了设置读取 IRP 的 MDL 地址外，驱动程序还必须设置下一个较低级别驱动程序的 i/o 堆栈位置。 驱动程序通过调用[**IoGetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)获取对下一个较低级别驱动程序的 i/o 堆栈位置的访问。 驱动程序设置 i/o 堆栈位置的以下成员：

<a href="" id="parameters-read-length"></a>**Parameters. 读取的长度**  
设置为读取缓冲区的大小（以字节为单位）。 此值必须大于或等于 HID 集合的 HIDP 的**InputReportByteLength**成员指定的值[ **\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)结构。

<a href="" id="parameters-read-key"></a>**Parameters。读取. 键**  
设置为零。

<a href="" id="parameters-read-byteoffset-quadpart"></a>**ByteOffset. QuadPart**  
设置为零。

<a href="" id="majorfunction"></a>**MajorFunction**  
设置为 IRP\_MJ\_读取。

<a href="" id="fileobject"></a>**FileObject**  
设置为表示 HID 集合上打开的文件的文件对象指针。

驱动程序获得输入报告后，它可以访问控制数据，如[解释 HID 报告](interpreting-hid-reports.md)中所述。

### <a href="" id="using-ioctl-hid-get-xxx-requests"></a>使用 IOCTL\_HID\_获取\_Xxx 请求

驱动程序可以使用以下 i/o 请求从 HID 集合中获取最新的输入和功能报告：

<a href="" id="ioctl-hid-get-input-report"></a>[**IOCTL\_HID\_获取\_输入\_报表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_input_report)  
从 HID 集合（Windows XP 及更高版本）返回输入报告。

<a href="" id="ioctl-hid-get-feature"></a>[**IOCTL\_HID\_获取\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_feature)  
从 HID 集合返回功能报告。

驱动程序可以请求特定报表的返回。 若要使用这些 i/o 请求来检索特定报表，驱动程序首先会分配输出报表缓冲区，然后将缓冲区初始化为零，并将缓冲区中的第一个字节设置为特定的报表 ID。 有关详细信息，请参阅[解释 HID 报表](interpreting-hid-reports.md)。

 

 




