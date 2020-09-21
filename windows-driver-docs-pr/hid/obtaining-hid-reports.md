---
title: 获取 HID 报告
description: 获取 HID 报告
ms.assetid: b6312dce-39af-4fff-b17d-4a50b9ab823b
keywords:
- 报告 WDK HID，获取
- ReadFile WDK HID
- IRP_MJ_READ 请求 WDK HID
- IOCTL_HID_GET_Xxx 请求 WDK HID
- HID 报告 WDK，获取
ms.date: 09/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 697875e66da157459e9753a718b6826d9a6e9d57
ms.sourcegitcommit: 8835925c6a88efc301dc5e8bd9bca87082416eb6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "90777595"
---
# <a name="obtaining-hid-reports"></a>获取 HID 报告

本部分介绍用户模式的应用程序和内核模式驱动程序如何从 [hid 集合](hid-collections.md)获取 hid 报表。

## <a name="obtaining-hid-reports-by-user-mode-applications"></a>通过用户模式应用程序获取 HID 报表

本主题介绍如何通过使用 [ReadFile](/windows/win32/api/fileapi/nf-fileapi-readfile) 或 **HidD_Get**Xxx 例程的用户模式应用程序获取 HID 输入报告或 hid 功能报告。

但是，应用程序应该只使用 **HidD_Get**Xxx 例程来获取设备的当前状态。 如果应用程序尝试使用 [HidD_GetInputReport](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getinputreport) 连续获取输入报告，则报告可能会丢失。 此外，某些设备可能不支持 **HidD_GetInputReport**，如果使用此例程，则不会响应。

### <a name="using-readfile"></a>使用 ReadFile

应用程序使用 **CreateFile** 获取的打开文件句柄，以打开集合中的文件。 当应用程序调用 **ReadFile**时，无需指定重叠 i/o，因为 [HID 客户端驱动程序](keyboard-and-mouse-hid-client-drivers.md) 会将报告缓冲到环形缓冲区中。 但是，应用程序可以使用重叠 i/o 来具有多个未完成的读取请求。

### <a name="using-hidd_getxxx-routines"></a>使用 HidD_GetXxx 例程

应用程序可以使用以下 [HIDClass 支持例程](/windows-hardware/drivers/ddi/_hid/#hidclass-support-routines) 从 HID 集合中获取最新的输入报告和功能报告：

- [HidD_GetInputReport](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getinputreport) 返回 (Windows XP 及更高版本) 的 HID 集合中的输入报告。

- [HidD_GetFeature](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getfeature) 从 HID 集合返回功能报告。

应用程序可以请求特定报表的返回。 若要使用这些例程检索特定报表，应用程序需要分配报表输出缓冲区，并将缓冲区初始化为零，并将缓冲区中的第一个字节设置为特定的报表 ID。 有关详细信息，请参阅 [初始化 HID 报表](initializing-hid-reports.md)。

## <a name="obtaining-hid-reports-by-kernel-mode-drivers"></a>通过内核模式驱动程序获取 HID 报表

本主题讨论内核模式驱动程序应如何使用 [IRP_MJ_READ](/windows-hardware/drivers/ifs/irp-mj-read) 请求作为持续获取 HID 输入报告的主要方法。

连续读取请求按从集合接收输入报告的顺序返回输入报告。 驱动程序还可以使用 **IOCTL_HID_GET_Xxx** 请求来获取输入和功能报告。 但是，驱动程序应仅使用这些 i/o 请求来获取设备的当前状态。 如果驱动程序尝试使用 [IOCTL_HID_GET_INPUT_REPORT](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_input_report) 连续获取输入报告，则报告可能会丢失。 此外，某些设备可能不支持 **IOCTL_HID_GET_INPUT_REPORT**，如果使用此请求，则将不会响应。

### <a name="using-irp_mj_read-requests"></a>使用 IRP_MJ_READ 请求

对于 Windows XP 及更高版本的非 WDM Windows 2000 驱动程序和驱动程序，可以对设备使用单个 IRP 来处理所有读取请求。 但是，Windows 2000 WDM 驱动程序必须为每个读取请求分配新的 IRP。 有关如何使用和重用 Irp 的一般信息，请参阅 [处理 irp](/windows-hardware/drivers/kernel/handling-irps) 和 [重用 irp](/windows-hardware/drivers/kernel/reusing-irps)。

如果驱动程序重用 IRP，则 IRP 的 [IoCompletion](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程应完成状态为 **STATUS_MORE_PROCESSING_REQUIRED** (的请求，而不释放 irp) 。 当驱动程序不再需要 IRP 时，应通过调用 [IoCompleteRequest](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 和 [IoFreeIrp](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)来完成并释放 irp。 例如，驱动程序通常可能在其 [卸载](/windows-hardware/drivers/kernel/unload-routine-functionality) 例程中完成并释放 IRP，或在删除设备之后。

如果驱动程序只对一个读取请求使用 IRP，IRP 的 **IoCompletion** 例程应完成并释放 irp，并返回 **STATUS_SUCCESS**。

在驱动程序可以请求输入报告之前，必须先从非分页内存池分配一个0初始化的输入报告缓冲区。 缓冲区的大小（以字节为单位）由 HID 集合的[HIDP_CAPS](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)结构的**InputReportByteLength**成员指定。 然后，驱动程序必须使用 MDL 来映射读取请求的输入报告缓冲区。 驱动程序调用 [IoAllocateMdl](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl) 为输入报告缓冲区分配 MDL，并将 read Irp 的 **irp >MdlAddress** 成员设置为输入报告缓冲区的 mdl 地址。 当不再需要报表缓冲区和 MDL 时，驱动程序应释放它。

除了设置读取 IRP 的 MDL 地址外，驱动程序还必须设置下一个较低级别驱动程序的 i/o 堆栈位置。 驱动程序通过调用 [IoGetNextIrpStackLocation](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)获取对下一个较低级别驱动程序的 i/o 堆栈位置的访问。 驱动程序设置 i/o 堆栈位置的以下成员：

**Parameters. 读取的长度**<br>
设置为读取缓冲区的大小（以字节为单位）。 此值必须大于或等于 HID 集合 [HIDP_CAPS](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps) 结构的 InputReportByteLength 成员所指定的值。

**Parameters。读取. 键**<br>
设置为零。

**ByteOffset. QuadPart**<br>
设置为零。

**MajorFunction**<br>
设置为 IRP_MJ_READ。

**FileObject**<br>
设置为表示 HID 集合上打开的文件的文件对象指针。

驱动程序获得输入报告后，它可以访问控制数据，如 [解释 HID 报告](interpreting-hid-reports.md)中所述。

### <a name="using-ioctl_hid_get_xxx-requests"></a>使用 IOCTL_HID_GET_Xxx 请求

驱动程序可以使用以下 i/o 请求从 HID 集合中获取最新的输入和功能报告：

- [IOCTL_HID_GET_INPUT_REPORT](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_input_report) 返回 (Windows XP 及更高版本) 的 HID 集合中的输入报告。

- [IOCTL_HID_GET_FEATURE](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_feature) 从 HID 集合返回功能报告。

驱动程序可以请求特定报表的返回。 若要使用这些 i/o 请求来检索特定报表，驱动程序首先会分配输出报表缓冲区，然后将缓冲区初始化为零，并将缓冲区中的第一个字节设置为特定的报表 ID。

有关详细信息，请参阅 [解释 HID 报表](interpreting-hid-reports.md)。
