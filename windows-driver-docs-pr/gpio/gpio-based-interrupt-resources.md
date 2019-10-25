---
title: 基于 GPIO 的中断资源
description: 将中断发送到常规用途 i/o （GPIO） pin 的外围设备的驱动程序会将 GPIO 中断获取为抽象的 Windows 中断资源。
ms.assetid: 65031C43-917D-4665-BD7F-97D3DDA0A918
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8233ecd148b5daf8539dc8ac95f650de3dd4641
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825036"
---
# <a name="gpio-based-interrupt-resources"></a>基于 GPIO 的中断资源


将中断发送到常规用途 i/o （GPIO） pin 的外围设备的驱动程序会将 GPIO 中断获取为抽象的 Windows 中断资源。 [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)（KMDF）驱动程序和[用户模式驱动程序框架](../wdf/overview-of-the-umdf.md)（UMDF）驱动程序通过其[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)事件回调函数接收这些资源。

使用基于 GPIO 的中断资源的外围设备驱动程序可以忽略低级别的实现细节，例如是否由 GPIO pin （而不是中断控制器）或处理器芯片上的中断 pin 生成中断。

基于 GPIO 的中断是**CmResourceTypeInterrupt**类型的资源。 此中断的配置参数包含在[**CM\_分部\_资源\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)结构（描述中断资源）的**u. 中断**成员中。 为了将中断服务例程（ISR）连接到中断，UMDF 或 KMDF 驱动程序将中断资源的[原始和已转换](https://docs.microsoft.com/windows-hardware/drivers/wdf/raw-and-translated-resources)说明提供给中断创建方法。

外围设备的 KMDF 或 UMDF 驱动程序调用[**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)方法，将 ISR 连接到设备上的中断。 此方法的输入参数之一是指向[**WDF\_中断\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)结构的指针，该结构包含中断的配置信息。 有关详细信息，请参阅[处理硬件中断](../wdf/handling-hardware-interrupts.md)。

如果外围设备驱动程序使用多个 GPIO 中断资源，则此驱动程序必须知道这些资源在作为输入参数提供给*EvtDevicePrepareHardware*的原始和转换资源列表中的显示顺序。函数或**OnPrepareHardware**方法。 这些列表中的资源按平台固件中描述的顺序显示，其中必须与驱动程序所需的顺序相匹配。

 

 




