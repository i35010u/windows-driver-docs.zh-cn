---
title: 如何启用调试而无需启动 ETW 跟踪会话
description: 如何启用调试而无需启动 ETW 跟踪会话
ms.assetid: d0487973-c66a-4ede-bc94-2e7e2060ab54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 072381d0cf6574056d28cb08088db4b944dec515
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359473"
---
# <a name="how-do-i-enable-debugging-without-starting-an-etw-trace-session"></a>如何在不启动 ETW 跟踪会话的情况下启用调试？


若要调试的问题，而无需启动 ETW 跟踪会话，添加**WPP\_调试**对源代码的宏定义。

下面是有关 WDK Tracedrv.sys 示例驱动程序示例：

```
#define WPP_DEBUG(b) DbgPrint b, DbgPrint("\n")
```

可用于大多数格式和参数**WPP\_调试**。 但是，不能使用扩展的格式规范，如 %！HEXDUMP ！ %，此宏。

另请参阅[如何将跟踪消息发送给用户模式下调试程序？](how-do-i-send-trace-messages-to-a-user-mode-debugger-.md)。

### <a name="span-idwhenusingthekerneldebuggerspanspan-idwhenusingthekerneldebuggerspanwhen-using-the-kernel-debugger"></a><span id="when_using_the_kernel_debugger"></span><span id="WHEN_USING_THE_KERNEL_DEBUGGER"></span>使用内核调试程序时

如果使用的内核调试程序，设置 WPP 控制结构的级别和标志值。

1.  找到 WPP 控制结构的地址，如下所示：
    ```
     kd>   x tracedrv!WPP_MAIN_CB    // tracedrv is the WPP instrumented driver
    9fbf3040 tracedrv!WPP_MAIN_CB = union WPP_PROJECT_CONTROL_BLOCK [1]
    kd>dt WPP_TRACE_CONTROL_BLOCK 9fbf3040  
    +0x000 Callback : 0x9fbf127c tracedrv!WppTraceCallback+0
    +0x004 ControlGuid : 0x9fbf206c _GUID {d58c126f-b309-11d1-969e-0000f875a5bc}
    +0x008 Next : (null) 
    +0x010 Logger : 0
    +0x018 RegistryPath : (null) 
    +0x01c FlagsLen : 0x1 ''
    +0x01d Level : 0x0 ''    <--- Set the Level
    +0x01e Reserved : 0
    +0x020 Flags : [1] 0x0  <--- Set the Flag
    ```

2.  设置为级别的值**5**和到标志**0xf**，按如下所示：
    ```
    kd>eb 9fbf305d 5    // setting the level value to 5
    ```

    ```
    kd>ed 9fbf3060 0xf    // setting the flag value to 0xf
    ```

3.  （Windows Vista 和更高版本的 Windows）启用要接收的消息，如下所示的筛选器掩码：
    ```
    kd>ed nt!Kd_DEFAULT_Mask 0xff
    ```

 

 





