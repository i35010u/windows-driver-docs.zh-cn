---
title: 使用 KMDF 和 UMDF 2 中的即时跟踪记录器 (IFR) 驱动程序
description: 从 Windows 10 开始，可以构建 WDF 驱动程序，以便获取其他驱动程序调试通过 Windows 软件跟踪预处理的信息。
ms.assetid: CA2A7ED3-4372-4EE9-8B04-042A8C864BD5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8deb7a4491b22e674fb1329dc7b5b8c42e17b59b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546346"
---
# <a name="using-inflight-trace-recorder-ifr-in-kmdf-and-umdf-2-drivers"></a>使用 KMDF 和 UMDF 2 中的即时跟踪记录器 (IFR) 驱动程序


从 Windows 10 开始，可以构建 KMDF 或 UMDF 驱动程序，以便获取其他驱动程序调试通过 Windows 软件跟踪预处理的信息。 从版本 1.15 KMDF 和 UMDF 2.15 版本开始，提供此功能，称为即时跟踪记录器 (IFR)。

即时跟踪记录器是的扩展[WPP 软件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556204)。 与 WPP 跟踪不同即时跟踪记录器继续正常运行附加的跟踪使用者。 框架将消息写入到一个循环缓冲区，和您的驱动程序还可以添加自己的消息。 每个驱动程序具有其自己的日志，因此多台设备与驱动程序共享一个日志相关联。

日志存储在不可分页的内存，因此可以在系统崩溃后恢复。 此外，小型转储文件中包含即时跟踪录制器日志。

**如何启用即时跟踪记录器，并从您的驱动程序发送消息**

1.  在 Microsoft Visual Studio 中，执行以下步骤：

    -   打开您的驱动程序项目的属性页。 在“解决方案资源管理器”中右键单击驱动程序项目，并选择**属性**。 在驱动程序的属性页中，单击**配置属性**，然后**Wpp 跟踪**。 上**常规**菜单中，设置**运行 WPP 跟踪**到**是**。

    -   导航到**属性-&gt;Wpp 跟踪-&gt;函数和宏选项**，然后选择**启用 WPP 记录器**。

    -   在相同菜单上，将**扫描配置数据**包含你的跟踪信息，例如 Trace.h 的文件。

2.  在调用 WPP 宏每个源代码文件中添加**\#包括**标识的指令[跟踪消息标头 (TMH) 文件](https://msdn.microsoft.com/library/windows/hardware/ff553926)。 文件名称的格式必须&lt;*驱动程序的源的文件名*&gt;**.tmh**。

    例如，如果您的驱动程序由两个源文件组成，称为*MyDriver1.c*并*MyDriver2.c*，然后*MyDriver1.c*必须包含：

    **\#include "MyDriver1.tmh"**

    并*MyDriver2.c*必须包含：

    **\#include "MyDriver2.tmh"**

    生成您在 Visual Studio 中的驱动程序时，WPP 预处理器生成。*tmh*文件。

3.  定义[WPP\_控制\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)标头文件中的宏。 此宏可定义 GUID 并[跟踪标志](https://msdn.microsoft.com/library/windows/hardware/ff553904)用于驱动程序的跟踪的消息。

    Osrusbfx2 驱动程序示例定义了单个控件的 GUID 和七个跟踪标志在 Trace.h 标头文件中，如下面的示例中所示：

    ```cpp
    #define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(OsrUsbFxTraceGuid, \
      (d23a0c5a,d307,4f0e,ae8e,E2A355AD5DAB), \
      WPP_DEFINE_BIT(DBG_INIT)          /* bit  0 = 0x00000001 */ \
      WPP_DEFINE_BIT(DBG_PNP)           /* bit  1 = 0x00000002 */ \
      WPP_DEFINE_BIT(DBG_POWER)         /* bit  2 = 0x00000004 */ \
      WPP_DEFINE_BIT(DBG_WMI)           /* bit  3 = 0x00000008 */ \
      WPP_DEFINE_BIT(DBG_CREATE_CLOSE)  /* bit  4 = 0x00000010 */ \
      WPP_DEFINE_BIT(DBG_IOCTL)         /* bit  5 = 0x00000020 */ \
      WPP_DEFINE_BIT(DBG_WRITE)         /* bit  6 = 0x00000040 */ \
      WPP_DEFINE_BIT(DBG_READ)          /* bit  7 = 0x00000080 */ \
    )
    ```

    在本示例中：

    -   **OsrUsbFxTraceGuid**是 {d23a0c5a-d307-4f0e-ae8e-E2A355AD5DAB} GUID 的友好名称。
    -   跟踪标志用于区分在生成的驱动程序句柄的 I/O 请求的不同类型的跟踪消息。

4.  您 （KMDF 和 UMDF 2） 的驱动程序必须调用[ **WPP\_INIT\_跟踪对内核模式驱动程序**](https://msdn.microsoft.com/library/windows/hardware/ff556193)驱动程序对象和注册表路径中，通常是从[**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff540807):

    ```cpp
    WPP_INIT_TRACING( DriverObject, RegistryPath );
    ```

    若要停用跟踪 KMDF 和 UMDF 2 驱动程序调用[ **WPP\_内核模式驱动程序的清除**](https://msdn.microsoft.com/library/windows/hardware/ff556183)从[ *EvtCleanupCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540840)或[ *EvtDriverUnload*](https://msdn.microsoft.com/library/windows/hardware/ff541694):

    ```cpp
    WPP_CLEANUP( WdfDriverWdmGetDriverObject( Driver ));
    ```

    [ **WPP\_清理**](https://msdn.microsoft.com/library/windows/hardware/ff556183)宏采用参数的类型 PDRIVER\_对象，因此，如果您的驱动程序[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807)失败，则可以跳过调用[ **WdfDriverWdmGetDriverObject** ](https://msdn.microsoft.com/library/windows/hardware/ff547218) ，并改为调用**WPP\_清理**用一个指针指向 WDM驱动程序对象。

    从 UMDF 2.15 版本开始，UMDF 驱动程序使用的初始化和清理跟踪这些宏的内核模式下签名。 这意味着调用 KMDF 和 UMDF 大致相同。

5.  使用[ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)宏，或[自定义的版本](https://msdn.microsoft.com/library/windows/hardware/ff542492)的驱动程序来创建跟踪消息中的宏。

    下面的示例演示如何 Osrusbfx2 驱动程序使用其**TraceEvents**函数在代码部分中的专门处理读取的请求：

    ```cpp
    if (Length > TEST_BOARD_TRANSFER_BUFFER_SIZE) {
        TraceEvents(TRACE_LEVEL_ERROR,
                    DBG_READ,
                    "Transfer exceeds %d\n",
                    TEST_BOARD_TRANSFER_BUFFER_SIZE);
     
        status = STATUS_INVALID_PARAMETER;
    }
    ```

    在调用**TraceEvents**生成的跟踪消息，如果启用了跟踪控制器**跟踪\_级别\_错误**级别和**DBG\_读取**跟踪标志。 该消息包含驱动程序定义常量的值**测试\_板\_传输\_缓冲区\_大小**。

6.  若要更改的驱动程序日志使用循环缓冲区大小，请修改**LogPages**以下注册表位置中的注册表值：

    <a href="" id="for-umdf-"></a>对于 UMDF:  

    **软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\Services\\&lt;YourDriver&gt;\\参数\\Wdf**

    <a href="" id="for-kmdf-"></a>对于 KMDF:  

    **HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\&lt;YourDriver&gt;\\Parameters\\Wdf**

    这是类型的值**REG\_DWORD**包含分配页中的日志缓冲区的大小。 有效值为 0x1 和 0x10 之间。

**对于 KMDF 驱动程序**

1.  通过键入加载 RCDRKD 命令 **.load rcdrkd.dll**在调试器中。
2.  使用[ **！ wdfkd.wdfldr** ](https://msdn.microsoft.com/library/windows/hardware/ff565803)扩展以显示有关当前动态绑定到 Windows 驱动程序框架 (WDF) 的驱动程序的信息。
3.  使用[ **！ rcdrkd.rcdrlogdump** ](https://msdn.microsoft.com/library/windows/hardware/hh920382)并[ **！ rcdrkd.rcdrcrashdump** ](https://msdn.microsoft.com/library/windows/hardware/hh920380)到驱动程序提供的查看消息。
4.  使用[ **！ wdfkd.wdflogdump** ](https://msdn.microsoft.com/library/windows/hardware/ff565805)或[ **！ wdfkd.wdfcrashdump** ](https://msdn.microsoft.com/library/windows/hardware/ff565682) ，请参阅该框架提供的消息。

**实时调试 UMDF 驱动程序**

1.  使用[ **！ wdfkd.wdfldr** ](https://msdn.microsoft.com/library/windows/hardware/ff565803)扩展以显示有关当前动态绑定到 WDF 驱动程序的信息。 查找您的用户模式驱动程序。 输入相关联的主机进程。
2.  类型 **！ wdfkd.wdflogdump**  *&lt;YourDriverName.dll&gt; &lt;标志&gt;* ，其中*&lt;标志&gt;* 是：

    -   0x1-合并框架和驱动程序日志
    -   0x2-驱动程序日志
    -   0x3-框架日志

    如果不没有指定驱动程序的任何驱动程序日志，该扩展将显示仅的框架日志。

**在 UMDF 驱动程序出现故障后查看即时跟踪录制器日志**

1. 从的 WinDbg 中，选择**文件-&gt;打开崩溃转储**，并指定你想要调试的小型转储文件。
2. 类型[ **！ wdfkd.wdfcrashdump  *&lt;YourDriverName.dll&gt; &lt;的驱动程序主机进程 ID&gt; &lt;选项&gt;*** ](https://msdn.microsoft.com/library/windows/hardware/ff565682)，其中*&lt;选项&gt;* 是：

   -   0x1-合并框架和驱动程序日志
   -   0x2-驱动程序日志
   -   0x3-框架日志

   如果未指定驱动程序， [ **！ wdfcrashdump** ](https://msdn.microsoft.com/library/windows/hardware/ff565682)显示所有驱动程序的信息。 如果未指定主机进程，并且只有一个，该扩展将单个主机进程。 如果未指定主机进程，并且没有多个，扩展会列出活动主机进程。

   如果存储的小型转储中的日志信息与输入的名称不匹配，小型转储不包含驱动程序的日志。

有关将跟踪消息添加到您的驱动程序的详细信息，请参阅[添加到驱动程序 WPP 宏](https://msdn.microsoft.com/library/windows/hardware/ff541243)。

## <a name="related-topics"></a>相关主题


[如何启用调试 UMDF 驱动程序](enabling-a-debugger.md)

[RCDRKD 扩展](https://msdn.microsoft.com/library/windows/hardware/hh920376)

[使用框架的事件记录器](using-the-framework-s-event-logger.md)

[使用 WPP 软件在 UMDF 驱动程序中进行跟踪](using-wpp-software-tracing-in-umdf-drivers.md)

 

 






