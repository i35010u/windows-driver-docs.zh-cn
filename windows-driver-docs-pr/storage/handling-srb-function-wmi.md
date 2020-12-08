---
title: 处理 SRB_FUNCTION_WMI
description: 处理 SRB_FUNCTION_WMI
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_WMI
- WMI WDK SCSI
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0ff92dcf3a746c9ddb8326023d273aa764172f4d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835195"
---
# <a name="handling-srb_function_wmi"></a>处理 SRB_FUNCTION_WMI

如果主机总线适配器 (HBA) 支持 [Windows Management Instrumentation](../kernel/implementing-wmi.md) (wmi) ，则端口驱动程序会将 wmi 请求发送到微型端口驱动程序。 HBA 通过将 [*PORT_CONFIGURATION_INFORMATION*](/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)结构的 "WmiDataProvider" 字段设置为 [**DriverEntry**](driverentry-of-scsi-miniport-driver.md)例程中的 **TRUE** 来指示它支持 WMI。

小型小型驱动程序的编写器准备用来处理 WMI 请求的小型端口，如下所示：

- 如果微型端口公开自定义数据块或事件块，则它应在 MOF 文件中定义此类块，并将其编译为微型端口的二进制图像中的二进制资源。 有关详细信息，请参阅 [Windows Management Instrumentation](../kernel/implementing-wmi.md)。

- 如 [SCSI 微型端口驱动程序例程](scsi-miniport-driver-routines.md)中所述，实现必需的和可选的 *HwScsiWmiXxx* 回调例程。

- 处理 SRB_FUNCTION_WMI。

如果微型端口驱动程序可能挂起了 WMI 请求，则其 **DriverEntry** 例程应该请求为 SRB 扩展分配内存，以便微型端口驱动程序可以在整个 SRB 处理过程中维护请求上下文。

在微型端口驱动程序处理其第一个 WMI 请求之前，必须在其设备扩展中分配 SCSI_WMILIB_CONTEXT 结构，并使用以下内容初始化结构：

- 微型端口驱动程序支持的数据和事件块的数量，包括系统在 *wmicore* 中定义的标准块以及微型端口驱动程序的自定义块（如果有）。

- 指向 SCSIWMIGUIDREGINFO 结构的数组的指针，每个支持的块各有一个。

- 入口点到微型端口驱动程序的 *HwScsiWmiXxx* 回调例程。 微型端口驱动程序必须至少提供 [*HwScsiWmiQueryReginfo*](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo) 例程和 [*HwScsiWmiQueryDataBlock*](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock) 例程的入口点。

除了将 PORT_CONFIGURATION_INFO 结构的 "WmiDataProvider" 字段设置为 **TRUE** 并实现所需的 *HwScsiWmiQueryReginfo* 例程以外，无需执行任何操作来注册其数据和事件块。 端口驱动程序负责向 WMI 内核组件注册微型端口驱动程序的块。

收到 SRB，其中 **函数** 成员设置为 SRB_FUNCTION_WMI 时，微型端口驱动程序的 [*HwScsiStartIo*](/previous-versions/windows/hardware/drivers/ff557323(v=vs.85)) 例程会执行以下操作：

- 如果请求可能挂起，则从 SRB 扩展分配一个 SCSIWMI_REQUEST_CONTEXT 结构; 如果请求永远无法挂起，则从堆栈中分配。

- 检查 **Srb->WMIFlags** 以确定请求是用于适配器还是逻辑单元。

- 调用 [**ScsiPortWmiDispatchFunction**](/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction) ，其中包含指向微型端口驱动程序的 SCSI_WMILIB_CONTEXT 的指针、其设备扩展和请求上下文，以及 SRB 中的以下参数：

    **Srb->WMISubFunction**

    **Srb->数据路径**

    **Srb->DataTransferLength**

    **Srb->DataBuffer**

- 当驱动程序完成处理请求时，将调用 [**ScsiPortWmiPostProcess**](/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmipostprocess) 。 如果驱动程序没有挂起请求，则可能会在回调中调用 **ScsiPortWmiPostProcess** 。 如果驱动程序 pends 请求，则在请求完成时应调用 **ScsiPortWmiPostProcess** 。

- 将 **Srb->DataTransferLength** 和 **Srb >SrbStatus** 分别设置为 [**ScsiPortWmiGetReturnSize**](/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmigetreturnsize) 和 [**ScsiPortWmiGetReturnStatus**](/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmigetreturnstatus)返回的值。

- 通过 **RequestComplete** 和 **NextRequest** 或 (**NextLuRequest**) 再次调用 [**ScsiPortNotification**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification) 。

有关 WMI 的详细信息，请参阅 [Windows Management Instrumentation](../kernel/implementing-wmi.md)。
