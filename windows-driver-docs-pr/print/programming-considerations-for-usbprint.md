---
title: USBPRINT 编程注意事项
description: USBPRINT 编程注意事项
ms.assetid: 351b3124-d584-4817-a5ce-09e16b54d41b
keywords:
- 打印机驱动程序 WDK USB
- USBPRINT
- USBMON
- USB 打印机 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53b4b909a861d9b57a95ead21fce0d001ebb3d39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356024"
---
# <a name="programming-considerations-for-usbprint"></a>USBPRINT 编程注意事项





Usbprint.sys USBMON，以及提供的接口非常类似于使用的并行打印机。 在许多情况下，就可以为单个打印机驱动程序或语言监视器，以在并行和无需修改的 USB 打印机上正常工作。 如果仅使用语言监视器[ **WritePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-writeport)并[ **ReadPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-readport)函数和[ **IOCTL\_PAR\_查询\_设备\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_query_device_id)请求，它将在 USB 和并行打印机之间移植。

在某些情况下，它可能需要将特定于供应商的请求发送到打印机，以便充分利用专用的打印机功能的语言监视器。 若要执行此操作，请使用[ **IOCTL\_USBPRINT\_供应商\_设置\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_vendor_set_command)并[ **IOCTL\_USBPRINT\_供应商\_获取\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_vendor_get_command)。 但请注意，使用这些 Ioctl 呈现语言监视器与并行端口监视器不兼容。

语言监视器通常没有他们管理的打印机的设备句柄的访问权限。 相反，它们必须位于语言监视器和总线驱动程序 (在此情况下 Usbprint.sys) 之间的端口监视器提供一个端口名称。 请参阅[语言和端口监视器交互](language-and-port-monitor-interaction.md)有关详细信息。 缺少设备句柄可防止直接调用设备总线驱动程序 Ioctl 语言监视器。 若要克服此限制，USBMON 实现[ **GetPrinterDataFromPort** ](https://docs.microsoft.com/previous-versions/ff550506(v=vs.85)) API，它允许通过 USBMON Ioctl 发给 USBPRINT 的语言监视器。

USB 打印堆栈与并行打印堆栈共享以下 Api 和 IOCTL:

[**WritePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-writeport)

[**ReadPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-readport)

[**IOCTL\_PAR\_查询\_设备\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_query_device_id)

以下 Ioctl 是特定于 USB 打印堆栈：

[**IOCTL\_USBPRINT\_GET\_1284\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_get_1284_id)

[**IOCTL\_USBPRINT\_GET\_LPT\_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_get_lpt_status)

[**IOCTL\_USBPRINT\_SOFT\_RESET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_soft_reset)

[**IOCTL\_USBPRINT\_VENDOR\_GET\_COMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_vendor_get_command)

[**IOCTL\_USBPRINT\_VENDOR\_SET\_COMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_vendor_set_command)

**请注意**   Usbprint.sys 不提供一种机制，用于从设备获取描述符，也不直接操作 USB 管道。

 

 

 




