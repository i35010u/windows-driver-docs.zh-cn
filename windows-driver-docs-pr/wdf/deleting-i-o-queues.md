---
title: 删除 I/O 队列
description: 删除 I/O 队列
ms.assetid: 7eb7a24d-de39-4e3d-865c-ebfb49d43519
keywords:
- I/O 队列 WDK KMDF，删除
- 临时 I/O 队列 WDK KMDF
- 正在删除 I/O 队列 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1eb3d6d35ce1cb3fe72fe4521c923b3a1ecbc3b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377459"
---
# <a name="deleting-io-queues"></a>删除 I/O 队列


基于框架的驱动程序必须删除只有某些他们创建的 I/O 队列。 如果创建了一个驱动程序[默认 I/O 队列](creating-i-o-queues.md)或通过调用配置的 I/O 队列[ **WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)，framework 删除队列驱动程序的对象。

例如，如果您希望每个设备的 I/O 队列存在，只要每个设备将仍保持插入到系统，您的驱动程序将创建其 I/O 队列中的其[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。 您的驱动程序可能会创建默认队列，接收除读取请求的所有请求和都接收只能单独队列读取请求。

该驱动程序不能删除这些 I/O 队列。 相反，该框架中删除的队列对象时删除队列所属的设备对象。 有关为什么您的驱动程序不能删除这些 I/O 队列的信息，请参阅下面的备注。

如果，但是，您的驱动程序将创建临时之外的 I/O 队列及其[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数，它必须调用[ **WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)若要删除这些队列，使用它们完成。 例如，提供的驱动程序[ *EvtDeviceFileCreate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)回调函数可能会创建一个 I/O 队列来处理与特定的框架文件对象相关联的 I/O 请求。 在本例中的驱动程序[ *EvtFileCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)回调函数必须调用[ **WdfIoQueuePurge** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurge)若要清除队列，然后调用**WdfObjectDelete**将其删除。

**请注意**  框架不允许使用其默认的 I/O 队列或任何驱动程序配置为接收特定类型的所有 I/O 请求的 I/O 队列中删除的驱动程序 (通过调用[ **WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching))。 如果您的驱动程序调用[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)若要删除队列对象，表示这些队列之一**WdfObjectDelete**返回，而不删除对象。 **WdfObjectDelete**不提供返回的状态，因此，框架将报告错误，仅当您[使用框架的验证器](using-kmdf-verifier.md)。

 

 

 





