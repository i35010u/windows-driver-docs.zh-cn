---
title: 发送 HID 报告
description: 发送 HID 报告
ms.assetid: a4571b79-847b-4db0-be02-ac2f922162bb
keywords:
- 报告 WDK HID，发送
- 发送报表
- WriteFile WDK HID
- IRP_MJ_WRITE 请求 WDK HID
- IOCTL_HID_SET_Xxx 请求 WDK HID
- HID 报告 WDK，发送
ms.date: 09/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 475772583fe7e072ca1a31662a3f12527028d81f
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734367"
---
# <a name="sending-hid-reports"></a>发送 HID 报告

本部分介绍用户模式应用程序和内核模式驱动程序如何将 HID 报表发送到 [hid 集合](hid-collections.md)。

## <a name="sending-hid-reports-by-user-mode-applications"></a>通过用户模式应用程序发送 HID 报表

用户模式应用程序应使用 [WriteFile](/windows/win32/api/fileapi/nf-fileapi-writefile) 作为其主要方法，将输出报告持续发送到 HID 集合。 应用程序还可以使用 **HidD_SetXxx** 例程将输出报告和功能报告发送到集合。 但是，应用程序应仅使用这些例程来设置集合的当前状态。 某些设备可能不支持 [HidD_SetOutputReport](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setoutputreport) ，如果使用此例程，它们将不会响应。

## <a name="using-writefile"></a>使用 WriteFile

应用程序应使用写入请求将输出报告发送到 HID 集合。 用户模式应用程序创建输出报表后，可以使用 [WriteFile](/windows/win32/api/fileapi/nf-fileapi-writefile)将输出报告发送到集合。

## <a name="using-hidd_setxxx-routines"></a>使用 HidD_SetXxx 例程

应用程序可以使用以下 [HIDClass 支持例程](/windows-hardware/drivers/ddi/_hid/#hidclass-support-routines) 将 hid 报告发送到 hid 集合：

[HidD_SetOutputReport](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setoutputreport))  (Windows XP 和更高版本将输出报告发送到 HID 集合。

[HidD_SetFeature](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setfeature) 向 HID 集合发送功能报表。

## <a name="sending-hid-reports-by-kernel-mode-drivers"></a>通过内核模式驱动程序发送 HID 报表

内核模式驱动程序应使用 [IRP_MJ_WRITE](../ifs/irp-mj-write.md) 请求作为其主要方法，将输出报告持续发送到 HID 集合。 驱动程序还可以使用 **IOCTL_HID_SET_Xxx** 请求将输出报告和功能报告发送到集合。 但是，驱动程序应仅使用这些 i/o 请求来设置集合的当前状态。 某些设备可能不支持 [IOCTL_HID_SET_OUTPUT_REPORT](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_set_output_report) ，并将在使用此请求时停止响应。

## <a name="using-irp_mj_write-requests"></a>使用 IRP_MJ_WRITE 请求

对于适用于 Windows XP 及更高版本的非 WDM Windows 2000 驱动程序和驱动程序，可以对发送到集合的所有写入请求使用单个 IRP。 但是，Windows 2000 WDM 驱动程序必须为每个写入请求分配新的 IRP。 有关如何使用和重用 Irp 的详细信息，请参阅 [处理 irp](../kernel/handling-irps.md) 和 [重用 irp](../kernel/reusing-irps.md)。

如果驱动程序重用写入 IRP，则 IRP 的  [IoCompletion](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程应完成状态为 **STATUS_MORE_PROCESSING_REQUIRED** (的请求，而不释放 IRP) 。 当驱动程序不再需要 IRP 时，应通过调用 [IoCompleteRequest](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 和 [IoFreeIrp](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)来完成并释放 irp。 例如，驱动程序通常可能在其 [卸载](../kernel/unload-routine-functionality.md) 例程中完成并释放 IRP，或在删除设备之后。

如果驱动程序只对一个写入请求使用 IRP，则 IRP 的 **IoCompletion** 例程应完成并释放 irp，并返回 **STATUS_SUCCESS**。

在发送输出报告之前，驱动程序必须先初始化并设置输出报告缓冲区，如 [初始化 HID 报告](initializing-hid-reports.md)中所述。 然后，该驱动程序必须使用 MDL 来映射写入请求的输出报告缓冲区。 驱动程序调用 [IoAllocateMdl](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl) 为输出报告分配 MDL，并将写入 **irp 的 irp >MdlAddress** 成员设置为输出报告缓冲区的 mdl 地址。 当不再需要报表缓冲区和 MDL 时，驱动程序必须将其释放。

除了设置写入 IRP 的 MDL 地址外，驱动程序还必须设置下一个较低级别驱动程序的 i/o 堆栈位置。 驱动程序通过调用 [IoGetNextIrpStackLocation](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)获取对下一个较低级别驱动程序的 i/o 堆栈位置的访问。 驱动程序设置 i/o 堆栈位置的以下成员：

**Parameters。写入长度**<br>
设置为输出报表的长度（以字节为单位）。 此设置应设置为 HID 集合的输出报告的长度，由集合的 HIDP_CAPS 结构的 OutputReportByteLength 成员指定。

**Parameters。写入密钥**<br>
设置为零。

**ByteOffset. QuadPart**<br>
设置为零。

**MajorFunction**<br>
设置为 IRP_MJ_WRITE。

**FileObject**<br>
设置为表示 HID 集合上打开的文件的文件对象指针。

## <a name="using-ioctl_hid_set_xxx-requests"></a>使用 IOCTL_HID_SET_Xxx 请求

驱动程序还可以使用以下 i/o 请求将输出和功能报告发送到 HID 集合：

[IOCTL_HID_SET_OUTPUT_REPORT](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_set_output_report)<br>
)  (Windows XP 和更高版本的集合中发送输出报告。

[IOCTL_HID_SET_FEATURE](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_set_feature)<br>
向集合发送功能报表。