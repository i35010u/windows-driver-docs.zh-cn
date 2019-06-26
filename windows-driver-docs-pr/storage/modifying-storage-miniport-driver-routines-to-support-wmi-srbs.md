---
title: 修改存储器微型端口驱动程序例程，使之支持 WMI SRB
description: 修改存储器微型端口驱动程序例程，使之支持 WMI SRB
ms.assetid: c3a222e8-dd02-4e45-b3e2-cec35d3abfdc
keywords:
- WMI Srb WDK 存储，修改例程以支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d13ab66ddaed2a2e7c0fba641bb0aff3f534963d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386180"
---
# <a name="modifying-storage-miniport-driver-routines-to-support-wmi-srbs"></a>修改存储器微型端口驱动程序例程，使之支持 WMI SRB


## <span id="ddk_modifying_storage_miniport_driver_routines_to_support_wmi_srbs_kg"></span><span id="DDK_MODIFYING_STORAGE_MINIPORT_DRIVER_ROUTINES_TO_SUPPORT_WMI_SRBS_KG"></span>


微型端口驱动程序支持 WMI Srb 之前，必须确保微型端口驱动程序包含所需[ **HwScsiWmiQueryReginfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)例程，它执行所指示的操作下面的例程：

[ **DriverEntry 的 SCSI 微型端口驱动程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)例程：

-   如果微型端口驱动程序使用 SCSI 端口 WMI 库，初始化[ **SCSI\_WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/ns-scsiwmi-_scsiwmilib_context)结构如下所示[使用 SCSI 端口 WMI库](using-the-scsi-port-wmi-library.md)。

-   指示端口驱动程序是否它应为 SRB 扩展分配内存。 微型端口驱动程序指示 SRB 扩展，应通过设置已分配**SrbExtensionSize**的成员[ **HW\_初始化\_数据 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)为非零值的结构。

[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))例程：

-   设置**WmiDataProvider**的成员[**端口\_配置\_信息 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)结构等于 **，则返回 TRUE**.

[ **HwScsiStartIo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))例程：

-   测试**函数**成员以查看它是否等于 SRB SRB\_函数\_WMI。 如果这种情况即 **，则返回 TRUE**，微型端口驱动程序必须处理类型 SRB [ **SCSI\_WMI\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_wmi_request_block)而不是比类型 SRB [ **SCSI\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)。

-   分配的内存[ **SCSIWMI\_请求\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/ns-scsiwmi-scsiwmi_request_context)结构，用于保存 SRB 上下文。 如果微型端口驱动程序可能会挂起 WMI 请求，从 SRB 扩展分配内存，以便微型端口驱动程序可以维护整个 SRB 处理过程的请求上下文。 否则，如果请求曾经将挂起没有机会，为分配内存上下文从堆栈。

-   检查**Srb**-&gt;**WMIFlags**以确定请求是否为适配器或逻辑单元。

-   调用 SCSI 端口 WMI 库调度例程[ **ScsiPortWmiDispatchFunction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction)。 有关如何调用此调度例程的说明，请参阅[使用 SCSI 端口 WMI 库](using-the-scsi-port-wmi-library.md)。

-   调用[ **ScsiPortWmiPostProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmipostprocess)之后处理请求，如果它是由驱动程序挂起。 如果该驱动程序没有未挂起请求，然后**ScsiPortWmiPostProcess**应调用在微型端口驱动程序回调例程中，而不是微型端口驱动程序的启动 I/O 例程。

-   设置**Srb**-&gt;**DataTransferLength**并**Srb**-&gt;**SrbStatus**返回的值为[ **ScsiPortWmiGetReturnSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmigetreturnsize)并[ **ScsiPortWmiGetReturnStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmigetreturnstatus)分别。

-   调用[ **ScsiPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)与**RequestComplete**并再次与**NextRequest**或 (**NextLuRequest**).

 

 




