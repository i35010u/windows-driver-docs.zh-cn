---
title: 获取由内核模式驱动程序的 HID 报表
description: 本主题讨论如何内核模式驱动程序应使用 IRP_MJ_READ 请求作为其主要方法用于持续获取 HID 输入的报表。
ms.assetid: 017481f1-8021-4fd5-ab8e-f09f6006e616
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1f8d7746827d9ea3bb369419e178e8aac1aacefa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375891"
---
# <a name="obtaining-hid-reports-by-kernel-mode-drivers"></a>获取由内核模式驱动程序的 HID 报表


本主题讨论如何使用内核模式驱动程序应[ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)持续获取 HID 输入报表中的请求作为其主要方法。

连续读取的请求中接收从集合的顺序返回输入的报表。 该驱动程序还可以使用 IOCTL\_HID\_获取\_*Xxx*请求以获取输入和功能的报表。 但是，驱动程序只应使用这些 I/O 请求以获取设备的当前状态。 如果驱动程序将尝试使用 IOCTL\_HID\_获取\_输入\_报告以持续获取输入的报表，报表可能会丢失。 此外，某些设备可能不支持 IOCTL\_HID\_获取\_输入\_报表，且会变得无响应，如果使用此请求。

以下部分提供的详细信息。

### <a href="" id="using-irp-ml-read-requests"></a>使用 IRP\_MJ\_读取的请求

Windows 2000 非 WDM 驱动程序和 Windows XP 和更高版本，驱动程序可用于单个 IRP 到设备的所有读取请求。 但是，Windows 2000 WDM 驱动程序必须为每个读取请求分配新 IRP。 有关如何使用和重复使用 Irp 的常规信息，请参阅[处理 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)并[重用 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/reusing-irps)。

如果驱动程序会 IRP，IRP 的重用[ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程应完成状态的状态请求\_详细\_处理\_必需 （而不免费 IRP）。 当驱动程序不再需要 IRP 时，应完成并释放通过调用 IRP [ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)并[ **IoFreeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)。 例如，驱动程序可能通常完成并释放 IRP 中的其[ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程，或设备之后被删除。

如果只有一个读取请求，IRP 的驱动程序使用使用 IRP **IoCompletion**例程应完成并释放 IRP，并返回状态\_成功。

驱动程序可以请求输入的报表之前，它必须首先分配从非分页的内存池初始化为零的输入的报表缓冲区。 通过指定的大小，以字节为单位的缓冲区**InputReportByteLength** HID 集合的成员[ **HIDP\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_caps)结构。 然后，驱动程序必须使用 MDL 要映射的读取请求的输入的报表缓冲区。 驱动程序调用[ **IoAllocateMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatemdl) MDL 分配对于输入的报表缓冲区，并设置读取 IRP 的**Irp-&gt;MdlAddress** MDL 地址的成员输入的报表的缓冲区中。 当不再需要时，该驱动程序应免费报表缓冲区和 MDL。

除了设置读取 IRP 的 MDL 地址，该驱动程序还必须设置下一步的较低级驱动程序的 I/O 堆栈位置。 驱动程序将通过调用获取 I/O 堆栈位置中的下一步的较低级驱动程序的访问权限[ **IoGetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation)。 该驱动程序设置的 I/O 堆栈位置的以下成员：

<a href="" id="parameters-read-length"></a>**Parameters.Read.Length**  
设置为，以字节为单位的读取缓冲区的大小。 这必须是大于或等于指定的值**InputReportByteLength** HID 集合的成员[ **HIDP\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_caps)结构。

<a href="" id="parameters-read-key"></a>**Parameters.Read.Key**  
设置为零。

<a href="" id="parameters-read-byteoffset-quadpart"></a>**Parameters.Read.ByteOffset.QuadPart**  
设置为零。

<a href="" id="majorfunction"></a>**MajorFunction**  
设置为 IRP\_MJ\_读取。

<a href="" id="fileobject"></a>**FileObject**  
将设置为表示 HID 集合上打开的文件的文件对象指针。

该驱动程序获取输入的报表后，它可以访问控制数据，如中所述[解释 HID 报表](interpreting-hid-reports.md)。

### <a href="" id="using-ioctl-hid-get-xxx-requests"></a>使用 IOCTL\_HID\_获取\_Xxx 请求

驱动程序可以使用以下的 I/O 请求 HID 集合中获取最新的输入和功能报表：

<a href="" id="ioctl-hid-get-input-report"></a>[**IOCTL\_HID\_获取\_输入\_报表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidclass/ni-hidclass-ioctl_hid_get_input_report)  
输入的报表从 HID 集合返回 （Windows XP 和更高版本）。

<a href="" id="ioctl-hid-get-feature"></a>[**IOCTL\_HID\_获取\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidclass/ni-hidclass-ioctl_hid_get_feature)  
返回从 HID 集合的功能报表。

驱动程序可以请求返回特定报表。 若要检索使用这些 I/O 请求的特定报表，该驱动程序首先分配输出报表缓冲区，则零初始化缓冲区，并设置为特定的报表 id。 缓冲区中的第一个字节 有关详细信息，请参阅[解释 HID 报表](interpreting-hid-reports.md)。

 

 




