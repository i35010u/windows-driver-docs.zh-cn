---
title: 获取有关常规 I/O 目标的信息
description: 获取有关常规 I/O 目标的信息
ms.assetid: 70ae920e-de2d-4014-bae4-74058b26e7c0
keywords:
- 常规 I/O 有关面向 WDK KMDF，信息
- WDK KMDF，常规 I/O 目标的状态信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf5d87c4e59010fd69377ca112233415028d816f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534487"
---
# <a name="obtaining-information-about-a-general-io-target"></a>获取有关常规 I/O 目标的信息


若要获取的 I/O 目标有关的信息，您的驱动程序可以调用 I/O 目标对象定义的以下方法：

<a href="" id="---------wdfiotargetgetdevice--------"></a>[**WdfIoTargetGetDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548625)  
返回与本地或远程 I/O 目标相关联的 framework 设备对象。

<a href="" id="wdfiotargetquerytargetproperty-or-wdfiotargetallocandquerytargetproperty"></a>[**WdfIoTargetQueryTargetProperty**](https://msdn.microsoft.com/library/windows/hardware/ff548646) or [**WdfIoTargetAllocAndQueryTargetProperty**](https://msdn.microsoft.com/library/windows/hardware/ff548585)  
检索与本地或远程 I/O 目标的设备相关联的设备属性。

<a href="" id="---------wdfiotargetgetstate--------"></a>[**WdfIoTargetGetState**](https://msdn.microsoft.com/library/windows/hardware/ff548631)  
返回的状态信息的本地或远程 I/O 目标。

<a href="" id="---------wdfiotargetwdmgettargetdeviceobject--------"></a>[**WdfIoTargetWdmGetTargetDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff548682)  
返回一个指向与本地或远程 I/O 目标相关联的 Windows 驱动程序模型 (WDM) 设备对象。

<a href="" id="---------wdfiotargetwdmgettargetphysicaldevice--------"></a>[**WdfIoTargetWdmGetTargetPhysicalDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548691)  
返回一个指向 WDM 物理设备 (PDO) 对象，该对象表示远程 I/O 目标设备。

<a href="" id="---------wdfiotargetwdmgettargetfileobject--------"></a>[**WdfIoTargetWdmGetTargetFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548686)  
返回一个指向与远程 I/O 目标相关联的 WDM 文件对象。

<a href="" id="wdfiotargetwdmgettargetfilehandle"></a>[**WdfIoTargetWdmGetTargetFileHandle**](https://msdn.microsoft.com/library/windows/hardware/ff548683)  
返回的句柄与远程 I/O 目标相关联的文件。

 

 





