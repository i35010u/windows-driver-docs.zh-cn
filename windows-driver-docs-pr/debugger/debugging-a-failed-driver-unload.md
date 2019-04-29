---
title: 调试失败的驱动程序卸载
description: 调试失败的驱动程序卸载
ms.assetid: df4b6082-8236-4a7f-80f4-6c33dc8e887a
keywords:
- 驱动程序卸载失败
- 驱动程序卸载调试
- 卸载失败
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87184ea0f1a34ae27942ee82b30c9cd73ba9019f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324607"
---
# <a name="debugging-a-failed-driver-unload"></a>调试失败的驱动程序卸载


## <span id="ddk_debugging_a_failed_driver_unload_dbg"></span><span id="DDK_DEBUGGING_A_FAILED_DRIVER_UNLOAD_DBG"></span>


如果不存在到泄漏的引用驱动程序将不卸载**DeviceObject**或**DriverObject**。 这是故障的驱动程序卸载的一个常见原因。

除了**IoCreateDevice**，有几个函数采用对引用**DriverObject**并**DeviceObject**。 如果不遵循的准则来使用函数，您将得到泄漏引用。

下面是举例说明如何调试此问题。 尽管**DeviceObject**使用在此示例中，此技术是有效的所有对象。

**修复了驱动程序无法卸载**

1.  驱动程序调用的后面放置一个断点**IoCreateDevice**。 获取**DeviceObject**地址。

2.  使用查找对象标头[ **！ 对象**](-object.md)此对象地址上的扩展：

    ```dbgcmd
    kd> !object 81a578c0 
    Object: 81a578c0  Type: (81bd0e70) Device
        ObjectHeader: 81a578a8
        HandleCount: 0  PointerCount: 3
        Directory Object: e1001208  Name: Serial0 
    ```

    中的第一个变量**ObjectHeader**是*指针计数*或*引用计数*。

3.  在指针上放置一个写断点计数，请使用**ObjectHeader**的地址：

    ```dbgcmd
    kd> ba w4 81a578a8 "k;g" 
    ```

4.  使用[ **g （转向）**](g--go-.md)。 调试器将生成日志。

5.  查找不匹配/取消引用引用对-具体而言，缺少取消引用。 (请注意， **ObReferenceObject**为深入了解内核宏实现。)

 

 





