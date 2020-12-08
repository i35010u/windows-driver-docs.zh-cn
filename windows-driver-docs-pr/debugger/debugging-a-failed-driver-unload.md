---
title: 调试失败的驱动程序卸载
description: 调试失败的驱动程序卸载
keywords:
- 驱动程序卸载失败
- 驱动程序卸载调试
- 卸载失败
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a51f0ccf1e899bbb7a2b24dafd7dca0646844f70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803635"
---
# <a name="debugging-a-failed-driver-unload"></a>调试失败的驱动程序卸载


## <span id="ddk_debugging_a_failed_driver_unload_dbg"></span><span id="DDK_DEBUGGING_A_FAILED_DRIVER_UNLOAD_DBG"></span>


如果存在对 **DeviceObject** 或 **DriverObject** 的泄漏引用，驱动程序将不会卸载。 这是驱动程序卸载失败的常见原因。

除了 **IoCreateDevice** 之外，还有几个函数引用了 **DriverObject** 和 **DeviceObject**。 如果未遵循使用函数的准则，最终将泄露引用。

下面是如何调试此问题的示例。 尽管本示例中使用了 **DeviceObject** ，但此方法适用于所有对象。

**修复卸载失败的驱动程序**

1.  在驱动程序调用 **IoCreateDevice** 之后立即放置一个断点。 获取 **DeviceObject** 地址。

2.  使用此对象地址上的 [**！对象**](-object.md) 扩展查找对象标头：

    ```dbgcmd
    kd> !object 81a578c0 
    Object: 81a578c0  Type: (81bd0e70) Device
        ObjectHeader: 81a578a8
        HandleCount: 0  PointerCount: 3
        Directory Object: e1001208  Name: Serial0 
    ```

    **ObjectHeader** 中的第一个变量是 *指针计数* 或 *引用计数*。

3.  使用 **ObjectHeader** 的地址，在指针计数上放置写入断点：

    ```dbgcmd
    kd> ba w4 81a578a8 "k;g" 
    ```

4.  使用 [**g (中转)**](g--go-.md)。 调试器将生成一个日志。

5.  查找不匹配的引用/取消引用对--具体说来，缺少取消引用。  (请注意， **ObReferenceObject** 作为内核内的宏实现。 ) 

 

 





