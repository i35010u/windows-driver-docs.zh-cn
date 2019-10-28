---
title: 修改存储器微型端口驱动程序例程，使之支持 WMI SRB
description: 修改存储器微型端口驱动程序例程，使之支持 WMI SRB
ms.assetid: c3a222e8-dd02-4e45-b3e2-cec35d3abfdc
keywords:
- WMI SRBs WDK 存储，修改要支持的例程
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 70c268140086c01a1d72eb89ed5d87e3af41271b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841611"
---
# <a name="modifying-storage-miniport-driver-routines-to-support-wmi-srbs"></a>修改存储器微型端口驱动程序例程，使之支持 WMI SRB

在微型端口驱动程序可以支持 WMI SRBs 之前，必须确保微型端口驱动程序包含所需的[*HwScsiWmiQueryReginfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)例程，并为以下例程执行指定的操作：

[**DRIVERENTRY SCSI 微型端口驱动程序**](driverentry-of-scsi-miniport-driver.md)例程：

- 如果微型端口驱动程序使用 SCSI 端口 WMI 库，请根据[使用 Scsi 端口 Wmi 库](using-the-scsi-port-wmi-library.md)中所述初始化[SCSI_WMILIB_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-_scsiwmilib_context)结构。

- 向端口驱动程序指示它是否应为 SRB 扩展分配内存。 微型端口驱动程序指示应通过将[**HW_INITIALIZATION_DATA （SCSI）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)结构的**SrbExtensionSize**成员设置为非零值来分配 SRB 扩展。

[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))例程：

- 将[PORT_CONFIGURATION_INFORMATION （SCSI）](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)结构的**WmiDataProvider**成员设置为等于**TRUE**。

[*HwScsiStartIo*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))例程：

- 要查看 SRB 是否等于 SRB_FUNCTION_WMI 的测试**函数**成员。 如果此条件为**TRUE**，微型端口驱动程序必须处理[**SCSI_WMI_REQUEST_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_wmi_request_block)类型的 SRB 而不是 SRB 类型的[**SCSI_REQUEST_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)。

- 为[SCSIWMI_REQUEST_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-scsiwmi_request_context)结构分配内存以保存 SRB 上下文。 如果微型端口驱动程序可能会挂起 WMI 请求，请从 SRB 扩展分配内存，使微型端口驱动程序可以在整个 SRB 处理过程中保持请求上下文。 否则，如果请求不会被挂起，请从堆栈为上下文分配内存。

- 检查**Srb-> WMIFlags** ，确定请求是用于适配器还是逻辑单元。

- 调用 SCSI 端口 WMI 库调度例程[**ScsiPortWmiDispatchFunction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction)。 有关如何调用此调度例程的说明，请参阅[使用 SCSI 端口 WMI 库](using-the-scsi-port-wmi-library.md)。

- 处理请求后，如果该驱动程序挂起了该请求，请调用[**ScsiPortWmiPostProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmipostprocess) 。 如果驱动程序没有挂起请求，则应在微型端口驱动程序回调例程中调用**ScsiPortWmiPostProcess** ，而不是在微型端口驱动程序的启动 i/o 例程中调用。

- 将 **> Srb DataTransferLength**和**Srb > SrbStatus**分别设置为[**ScsiPortWmiGetReturnSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmigetreturnsize)和[**ScsiPortWmiGetReturnStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmigetreturnstatus)返回的值。

- 通过**RequestComplete**和**NextRequest**或（**NextLuRequest**）再次调用[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification) 。
