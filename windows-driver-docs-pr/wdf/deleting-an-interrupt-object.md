---
title: 删除中断对象
description: 删除中断对象
ms.assetid: B72DA452-B22F-47CD-8C5D-E741F09F556E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 659ac2e58b4cd1a9536eb179d459e46cfabf979a
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210475"
---
# <a name="deleting-an-interrupt-object"></a>删除中断对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

如果驱动程序通过调用[**IWDFDevice3：： CreateInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)创建中断对象，则驱动程序无需删除中断对象。 框架自动删除中断对象，因为中断对象是框架设备对象的子对象。

框架使用以下规则：

-   如果驱动程序从其[**OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)回调方法中调用[**CreateInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt) ，则框架将在驱动程序从其[**OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onreleasehardware)回调返回后删除中断对象。

-   如果驱动程序从其[**OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调方法中调用[**CreateInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt) ，则在删除设备时，框架会删除中断对象。

或者，驱动程序可以随时调用[**IWDFObject：:D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)删除中断对象。 由于驱动程序无法在[**OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)或[**OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)之外创建新的中断对象，因此不应使用手动删除该对象，除非该驱动程序必须在框架删除该对象之前删除它。

 

 





