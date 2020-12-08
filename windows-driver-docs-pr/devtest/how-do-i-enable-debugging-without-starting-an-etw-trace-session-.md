---
title: 如何实现在不启动 ETW 跟踪会话的情况下启用调试
description: 如何实现在不启动 ETW 跟踪会话的情况下启用调试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14b259c8c9ab344f7296ae81e56487d6912cea3e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826123"
---
# <a name="how-do-i-enable-debugging-without-starting-an-etw-trace-session"></a>如何在不启动 ETW 跟踪会话的情况下启用调试？


若要在不启动 ETW 跟踪会话的情况下调试问题，请在源代码中添加一个 **WPP \_ 调试** 宏定义。

下面是 WDK Tracedrv.sys 示例驱动程序的示例：

```
#define WPP_DEBUG(b) DbgPrint b, DbgPrint("\n")
```

大多数格式和参数可与 **WPP \_ 调试** 一起使用。 但是，不能使用扩展格式规范，例如%！此宏的 HEXDUMP！%。

另请参阅 [如何实现将跟踪消息发送到用户模式调试器？](how-do-i-send-trace-messages-to-a-user-mode-debugger-.md)。

### <a name="span-idwhen_using_the_kernel_debuggerspanspan-idwhen_using_the_kernel_debuggerspanwhen-using-the-kernel-debugger"></a><span id="when_using_the_kernel_debugger"></span><span id="WHEN_USING_THE_KERNEL_DEBUGGER"></span>使用内核调试器时

如果使用的是内核调试器，请为 WPP 控件结构设置级别和标志值。

1.  找到 WPP 控件结构的地址，如下所示：
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

2.  将级别的值设置为 **5** ，将标志设置为 **0xf**，如下所示：
    ```
    kd>eb 9fbf305d 5    // setting the level value to 5
    ```

    ```
    kd>ed 9fbf3060 0xf    // setting the flag value to 0xf
    ```

3.   (Windows Vista 和更高版本的 Windows) 启用筛选器掩码来接收消息，如下所示：
    ```
    kd>ed nt!Kd_DEFAULT_Mask 0xff
    ```

 

 





