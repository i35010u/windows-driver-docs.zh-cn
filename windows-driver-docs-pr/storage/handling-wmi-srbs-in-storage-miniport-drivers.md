---
title: 处理存储器微型端口驱动程序中的 WMI SRB
description: 处理存储器微型端口驱动程序中的 WMI SRB
ms.assetid: 92b78611-7e6f-4d77-9133-635df96584f0
keywords:
- 存储微型端口驱动程序 WDK，WMI SRBs
- 微型端口驱动程序 WDK 存储，WMI SRBs
- WMI SRBs WDK 存储，关于 WMI SRBs
- WMI SRBs WDK 存储
- SRB WMI 支持 WDK 存储
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6bf7f23c1a2c824962418eb0b28bbd74a9dbd197
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252407"
---
# <a name="handling-wmi-srbs-in-storage-miniport-drivers"></a>处理存储器微型端口驱动程序中的 WMI SRB

报告主机总线适配器（HBA）或允许 WMI 客户端与 HBA 的存储微型端口驱动程序交互的 WMI 接口通常要求微型端口驱动程序充当 WMI 提供程序。 存储微型端口驱动程序注册为 WMI 提供程序后，必须准备好处理一种称为 Windows Management Instrumentation （WMI） SCSI 请求块（[SCSI_WMI_REQUEST_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_wmi_request_block)）的特殊 SCSI 请求块（SRB）。

若要准备好存储微型端口驱动程序来处理 WMI SRBs，请完成以下步骤：

1. 设计和编译一个托管对象格式（MOF）文件，该文件描述了不由系统提供的 MOF 文件定义的 WMI 架构的这些部分。

    有关 MOF 语法的说明，请参阅[WMI 数据和事件块的 MOF 语法](https://docs.microsoft.com/windows-hardware/drivers/kernel/mof-syntax-for-wmi-data-and-event-blocks)。

2. 实现微型端口驱动程序回调例程。

    SCSI 端口 WMI 库可简化对小型端口驱动程序的 WMI SRBs 的处理。 若要使用 SCSI 端口 WMI 库，请实现[SCSI 微型端口驱动程序例程](scsi-miniport-driver-routines.md)中所述的*HwScsiWmiXxx*回调例程。

3. 将所需的代码添加到微型端口驱动[**程序的 DriverEntry 的 SCSI 微型端口驱动程序**](driverentry-of-scsi-miniport-driver.md)例程。

4. 向微型端口驱动程序的[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))例程添加所需的代码。

5. 向微型端口驱动程序的[*HwScsiStartIo*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))例程添加所需的代码。

有关实现前面的步骤的信息，请参阅以下主题：

- [端口驱动程序如何处理 WMI 请求](how-the-port-driver-processes-wmi-requests.md)

- [使用 SCSI 端口 WMI 库](using-the-scsi-port-wmi-library.md)

- [设计 WMI 微型端口驱动程序回调例程](designing-wmi-miniport-driver-callback-routines.md)

- [修改存储微型端口驱动程序例程以支持 WMI SRBs](modifying-storage-miniport-driver-routines-to-support-wmi-srbs.md)
