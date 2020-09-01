---
title: 获取有关常规 I/O 目标的信息
description: 获取有关常规 I/O 目标的信息
ms.assetid: 70ae920e-de2d-4014-bae4-74058b26e7c0
keywords:
- 一般 i/o 目标 WDK KMDF，有关
- 状态信息 WDK KMDF，一般 i/o 目标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb652560bc99dda170df081ee96eab8a02e6dee1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184611"
---
# <a name="obtaining-information-about-a-general-io-target"></a>获取有关常规 I/O 目标的信息


若要获取有关 i/o 目标的信息，驱动程序可以调用 i/o 目标对象定义的以下方法：

<a href="" id="---------wdfiotargetgetdevice--------"></a>[**WdfIoTargetGetDevice**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetgetdevice)  
返回与本地或远程 i/o 目标相关联的框架设备对象。

<a href="" id="wdfiotargetquerytargetproperty-or-wdfiotargetallocandquerytargetproperty"></a>[**WdfIoTargetQueryTargetProperty**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetquerytargetproperty)或[ **WdfIoTargetAllocAndQueryTargetProperty**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetallocandquerytargetproperty)  
检索与本地或远程 i/o 目标设备关联的设备属性。

<a href="" id="---------wdfiotargetgetstate--------"></a>[**WdfIoTargetGetState**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetgetstate)  
返回本地或远程 i/o 目标的状态信息。

<a href="" id="---------wdfiotargetwdmgettargetdeviceobject--------"></a>[**WdfIoTargetWdmGetTargetDeviceObject**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetdeviceobject)  
返回一个指针，该指针指向与本地或远程 i/o 目标相关联的 Windows 驱动模型 (WDM) 设备对象。

<a href="" id="---------wdfiotargetwdmgettargetphysicaldevice--------"></a>[**WdfIoTargetWdmGetTargetPhysicalDevice**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetphysicaldevice)  
返回一个指针，该指针指向表示远程 i/o 目标设备 (PDO) 的 WDM 物理设备对象。

<a href="" id="---------wdfiotargetwdmgettargetfileobject--------"></a>[**WdfIoTargetWdmGetTargetFileObject**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfileobject)  
返回一个指针，该指针指向与远程 i/o 目标相关联的 WDM 文件对象。

<a href="" id="wdfiotargetwdmgettargetfilehandle"></a>[**WdfIoTargetWdmGetTargetFileHandle**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfilehandle)  
返回与远程 i/o 目标相关联的文件的句柄。

 

