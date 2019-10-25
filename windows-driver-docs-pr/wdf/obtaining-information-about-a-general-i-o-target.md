---
title: 获取有关常规 I/O 目标的信息
description: 获取有关常规 I/O 目标的信息
ms.assetid: 70ae920e-de2d-4014-bae4-74058b26e7c0
keywords:
- 一般 i/o 目标 WDK KMDF，有关
- 状态信息 WDK KMDF，一般 i/o 目标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 743f41e1aa339d767408ff41ec95b58e070038b2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843140"
---
# <a name="obtaining-information-about-a-general-io-target"></a>获取有关常规 I/O 目标的信息


若要获取有关 i/o 目标的信息，驱动程序可以调用 i/o 目标对象定义的以下方法：

<a href="" id="---------wdfiotargetgetdevice--------"></a>[**WdfIoTargetGetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetgetdevice)  
返回与本地或远程 i/o 目标相关联的框架设备对象。

<a href="" id="wdfiotargetquerytargetproperty-or-wdfiotargetallocandquerytargetproperty"></a>[**WdfIoTargetQueryTargetProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetquerytargetproperty)或[ **WdfIoTargetAllocAndQueryTargetProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetallocandquerytargetproperty)  
检索与本地或远程 i/o 目标设备关联的设备属性。

<a href="" id="---------wdfiotargetgetstate--------"></a>[**WdfIoTargetGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetgetstate)  
返回本地或远程 i/o 目标的状态信息。

<a href="" id="---------wdfiotargetwdmgettargetdeviceobject--------"></a>[**WdfIoTargetWdmGetTargetDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetdeviceobject)  
返回一个指针，该指针指向与本地或远程 i/o 目标相关联的 Windows 驱动模型（WDM）设备对象。

<a href="" id="---------wdfiotargetwdmgettargetphysicaldevice--------"></a>[**WdfIoTargetWdmGetTargetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetphysicaldevice)  
返回一个指针，该指针指向表示远程 i/o 目标设备的 WDM 物理设备对象（PDO）。

<a href="" id="---------wdfiotargetwdmgettargetfileobject--------"></a>[**WdfIoTargetWdmGetTargetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfileobject)  
返回一个指针，该指针指向与远程 i/o 目标相关联的 WDM 文件对象。

<a href="" id="wdfiotargetwdmgettargetfilehandle"></a>[**WdfIoTargetWdmGetTargetFileHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfilehandle)  
返回与远程 i/o 目标相关联的文件的句柄。

 

 





