---
title: 删除 I/O 队列
description: 删除 I/O 队列
ms.assetid: 7eb7a24d-de39-4e3d-865c-ebfb49d43519
keywords:
- I/o 队列 WDK KMDF，删除
- 临时 i/o 队列 WDK KMDF
- 删除 i/o 队列 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 433ceb4fd52ca4ddc17319875fd0112ef79c8f0d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191566"
---
# <a name="deleting-io-queues"></a>删除 I/O 队列


基于框架的驱动程序必须仅删除其创建的某些 i/o 队列。 如果驱动程序通过调用[**WdfDeviceConfigureRequestDispatching**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)来创建它所配置的[默认 i/o 队列](creating-i-o-queues.md)或 i/o 队列，则该框架将删除该驱动程序的队列对象。

例如，如果你希望每个设备的 i/o 队列都已存在，只要每个设备仍插入系统，你的驱动程序就会在其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数中创建其 i/o 队列。 你的驱动程序可能会创建一个默认队列，用于接收除读取请求之外的所有请求和仅接收读取请求的单独队列。

驱动程序无法删除这些 i/o 队列。 相反，当队列对象删除队列所属的设备对象时，框架会将其删除。 有关驱动程序无法删除这些 i/o 队列的原因的信息，请参阅以下说明。

然而，如果你的驱动程序在其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数之外创建了临时 i/o 队列，则它必须调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) ，以在使用完它们后删除这些队列。 例如，提供 [*EvtDeviceFileCreate*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create) 回调函数的驱动程序可能会创建一个 i/o 队列来处理与特定框架文件对象相关联的 i/o 请求。 在这种情况下，驱动程序的 [*EvtFileCleanup*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup) 回调函数必须调用 [**WdfIoQueuePurge**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurge) 来清除队列，然后调用 **WdfObjectDelete** 将其删除。

**注意**   此框架不允许驱动程序删除其默认 i/o 队列，或驱动程序配置的任何 i/o 队列，以便通过调用[**WdfDeviceConfigureRequestDispatching**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)) 接收特定类型 (的所有 i/o 请求。 如果你的驱动程序调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 来删除表示其中某个队列的队列对象，则 **WdfObjectDelete** 将返回，而不会删除该对象。 **WdfObjectDelete** 不提供返回状态，因此，只有在 [使用框架的验证](using-kmdf-verifier.md)程序时，框架才会报告错误。

 

 

