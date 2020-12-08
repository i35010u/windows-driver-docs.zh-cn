---
title: 处理存储器微型端口驱动程序中的 WMI SRB
description: 处理存储器微型端口驱动程序中的 WMI SRB
keywords:
- 存储微型端口驱动程序 WDK，WMI SRBs
- 微型端口驱动程序 WDK 存储，WMI SRBs
- WMI SRBs WDK 存储，关于 WMI SRBs
- WMI SRBs WDK 存储
- SRB WMI 支持 WDK 存储
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4220c93eb170684a4e0d76120f11a7dae3b0f227
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835193"
---
# <a name="handling-wmi-srbs-in-storage-miniport-drivers"></a>处理存储器微型端口驱动程序中的 WMI SRB

用于报告有关主机总线适配器的信息 (HBA) 或允许 WMI 客户端与 HBA 的存储微型端口驱动程序交互的 WMI 接口，通常要求微型端口驱动程序充当 WMI 提供程序。 在存储微型端口驱动程序注册为 WMI 提供程序后，必须准备好处理一种特殊类型的 SCSI 请求块 (SRB) 称为 Windows Management Instrumentation (WMI) SCSI 请求[块 (SCSI_WMI_REQUEST_BLOCK) 。](/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_wmi_request_block)

若要准备好存储微型端口驱动程序来处理 WMI SRBs，请完成以下步骤：

1. 设计和编译一个托管对象格式 (MOF) 文件，该文件描述未由系统提供的 MOF 文件定义的 WMI 架构部分。

    有关 MOF 语法的说明，请参阅 [WMI 数据和事件块的 MOF 语法](../kernel/mof-syntax-for-wmi-data-and-event-blocks.md)。

2. 实现微型端口驱动程序回调例程。

    SCSI 端口 WMI 库可简化对小型端口驱动程序的 WMI SRBs 的处理。 若要使用 SCSI 端口 WMI 库，请实现 [SCSI 微型端口驱动程序例程](scsi-miniport-driver-routines.md)中所述的 *HwScsiWmiXxx* 回调例程。

3. 将所需的代码添加到微型端口驱动 [**程序的 DriverEntry 的 SCSI 微型端口驱动程序**](driverentry-of-scsi-miniport-driver.md) 例程。

4. 向微型端口驱动程序的 [*HwScsiFindAdapter*](/previous-versions/windows/hardware/drivers/ff557300(v=vs.85)) 例程添加所需的代码。

5. 向微型端口驱动程序的 [*HwScsiStartIo*](/previous-versions/windows/hardware/drivers/ff557323(v=vs.85)) 例程添加所需的代码。

有关实现前面的步骤的信息，请参阅以下主题：

- [端口驱动程序如何处理 WMI 请求](how-the-port-driver-processes-wmi-requests.md)

- [使用 SCSI 端口 WMI 库](using-the-scsi-port-wmi-library.md)

- [设计 WMI 微型端口驱动程序回调例程](designing-wmi-miniport-driver-callback-routines.md)

- [修改存储器微型端口驱动程序例程，使之支持 WMI SRB](modifying-storage-miniport-driver-routines-to-support-wmi-srbs.md)
