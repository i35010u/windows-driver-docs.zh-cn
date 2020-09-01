---
title: USBPRINT 编程注意事项
description: USBPRINT 编程注意事项
ms.assetid: 351b3124-d584-4817-a5ce-09e16b54d41b
keywords:
- 打印机驱动程序 WDK，USB
- USBPRINT
- USBMON
- USB 打印机 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0055acf24f05490db166ff0fefe4a2046603ae32
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207701"
---
# <a name="programming-considerations-for-usbprint"></a>USBPRINT 编程注意事项





Usbprint.sys 与 USBMON 一起提供了一个接口，该接口与并行打印机使用的接口非常类似。 在许多情况下，单个打印机驱动程序或语言监视器在无需修改的情况下，可以在并行打印机和 USB 打印机上正常工作。 如果语言监视器仅使用 [**WritePort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport) 和 [**ReadPort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport) 函数以及 [**IOCTL \_ PAR \_ 查询 \_ 设备 \_ ID**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_query_device_id) 请求，则它将可在 USB 和并行打印机之间移植。

在某些情况下，语言监视器可能需要对打印机进行特定于供应商的请求，才能利用特殊的打印机功能。 为此，请使用 [**ioctl \_ USBPRINT \_ 供应商 \_ SET \_ 命令**](/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_vendor_set_command) 和 [**ioctl \_ USBPRINT \_ 供应商 \_ GET \_ 命令**](/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_vendor_get_command)。 但请注意，使用这些 IOCTLs 会呈现与并行端口监视器不兼容的语言监视器。

对于正在管理的打印机，语言监视器通常无法访问设备句柄。 相反，它们有一个端口名称由端口监视器提供，后者位于语言监视器和总线驱动程序之间 ( # A0) 。 有关详细信息，请参阅 [语言和端口监视器交互](language-and-port-monitor-interaction.md) 。 缺少设备句柄会阻止语言监视器直接调用设备总线驱动程序 IOCTLs。 为了克服这一限制，USBMON 实现了 [**GetPrinterDataFromPort**](/previous-versions/ff550506(v=vs.85)) API，该 API 允许语言监视器通过 USBMON 向 USBPRINT 发出 IOCTLs。

USB 打印堆栈与并行打印堆栈共享以下 Api 和 IOCTL：

[**WritePort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport)

[**ReadPort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport)

[**IOCTL \_ PAR \_ 查询 \_ 设备 \_ ID**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_query_device_id)

以下 IOCTLs 特定于 USB 打印堆栈：

[**IOCTL \_ USBPRINT \_ GET \_ 1284 \_ ID**](/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_get_1284_id)

[**IOCTL \_ USBPRINT \_ 获取 \_ LPT \_ 状态**](/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_get_lpt_status)

[**IOCTL \_ USBPRINT \_ 软 \_ 重置**](/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_soft_reset)

[**IOCTL \_ USBPRINT \_ 供应商 \_ GET \_ 命令**](/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_vendor_get_command)

[**IOCTL \_ USBPRINT \_ 供应商 \_ SET \_ 命令**](/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_vendor_set_command)

**注意**   Usbprint.sys 不提供从设备中获取描述符的机制，也不提供直接操作 USB 管道的机制。

 

 

