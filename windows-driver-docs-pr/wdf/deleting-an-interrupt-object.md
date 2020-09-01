---
title: 删除中断对象
description: 删除中断对象
ms.assetid: B72DA452-B22F-47CD-8C5D-E741F09F556E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d4fb9b6bea4273907f8aa5ac7a205df065feeff
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191573"
---
# <a name="deleting-an-interrupt-object"></a>删除中断对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

如果驱动程序通过调用 [**IWDFDevice3：： CreateInterrupt**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)创建中断对象，则驱动程序无需删除中断对象。 框架自动删除中断对象，因为中断对象是框架设备对象的子对象。

框架使用以下规则：

-   如果驱动程序从其[**OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)回调方法中调用[**CreateInterrupt**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt) ，则框架将在驱动程序从其[**OnReleaseHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onreleasehardware)回调返回后删除中断对象。

-   如果驱动程序从其[**OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调方法中调用[**CreateInterrupt**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt) ，则在删除设备时，框架会删除中断对象。

或者，驱动程序可以随时调用 [**IWDFObject：:D eletewdfobject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) 删除中断对象。 由于驱动程序无法在 [**OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 或 [**OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)之外创建新的中断对象，因此不应使用手动删除该对象，除非该驱动程序必须在框架删除该对象之前删除它。

 

