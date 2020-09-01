---
title: 转发 I/O 请求
description: 转发 I/O 请求
ms.assetid: 75e007e3-1b97-44db-ac86-56aab78222a6
keywords:
- 转发 i/o 请求 WDK KMDF
- I/o 请求 WDK KMDF，转发
- 请求处理 WDK KMDF、转发 i/o 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22a14d3b4f1f3c261a4f541e2cc347eedfea40a8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189167"
---
# <a name="forwarding-io-requests"></a>转发 I/O 请求





当驱动程序收到无法处理的 i/o 请求时，通常会执行以下操作之一：

-   它将接收的请求转发到另一个驱动程序。

-   它会创建其他请求并将其发送到另一个驱动程序。

基于框架的驱动程序通过 [使用 i/o 目标](using-i-o-targets.md)转发请求，这些目标表示系统上的其他驱动程序。 驱动程序可以使用以下任一方法将请求转发到 i/o 目标：

-   驱动程序可以通过调用 [**WdfDeviceGetIoTarget**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetiotarget)，后跟 [**WdfRequestFormatRequestUsingCurrentType**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestformatrequestusingcurrenttype)，最后 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)，将 i/o 请求转发到下一个较低的驱动程序。

    仅当驱动程序接收到不需要在转发之前修改的请求时，此方法才有用。

-   驱动程序可以调用 [**WdfFdoInitSetFilter**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter) ，将自身注册为筛选器驱动程序。

    如果筛选器驱动程序未提供特定类型的 i/o 请求的 i/o 队列，框架会自动将该类型的请求转发到下一个较低的驱动程序。

-   通常，函数驱动程序会检查每个 i/o 请求的内容。 如果函数驱动程序无法处理请求，则它可能会修改请求并将其转发到 i/o 目标。 或者，它可能会创建一个或多个新请求，并将它们发送到 i/o 目标。

    框架的 i/o 目标对象定义了用于将 i/o 请求发送到其他驱动程序的几种方法。 例如，驱动程序可以调用 [**WdfIoTargetFormatRequestForRead**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread)，然后调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)来向 i/o 目标发送读取请求。 有关 i/o 目标的详细信息，请参阅 [使用 I/o 目标](using-i-o-targets.md)。

    通常，驱动程序编写器可能需要在向 i/o 目标发送请求之前指定请求的基础 WDM [i/o 堆栈位置](../kernel/i-o-stack-locations.md) 的内容。 对于这些情况，驱动程序可以在调用[**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)之前调用[**WdfRequestWdmFormatUsingStackLocation**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestwdmformatusingstacklocation) 。

有时，驱动程序必须向多个 i/o 目标发送相同的请求，通常是因为驱动程序必须将单个命令发送到其所有设备。 在向 i/o 目标发送请求之前，驱动程序可以调用 [**WdfRequestChangeTarget**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestchangetarget) 来验证 i/o 目标是否可访问。

驱动程序最终必须[完成](completing-i-o-requests.md)转发到 i/o 目标的每个请求，除非它在调用[**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)时设置[**WDF \_ 请求 \_ 发送 \_ 选项 \_ 发送 \_ 和 \_ 忘记**](/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_send_options_flags)标志。

请注意，当驱动程序转发请求时，框架不会将 framework 请求对象从发送驱动程序传输到接收驱动程序。 而是在接收请求的驱动程序中创建新的请求对象。 只有请求的基础 i/o 请求数据包 ([**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)) 会从一个驱动程序传输到另一个驱动程序。

 

