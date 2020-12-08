---
title: 在 KMDF 和 UMDF 2 驱动程序中使用即时跟踪记录器 (IFR)
description: 从 Windows 10 开始，可以生成 WDF 驱动程序，以便它通过 Windows 软件跟踪预处理获取其他驱动程序调试信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adef6ba741fb8d06a7fb5f394c4b7fccc7ea229e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785409"
---
# <a name="using-inflight-trace-recorder-ifr-in-kmdf-and-umdf-2-drivers"></a>在 KMDF 和 UMDF 2 驱动程序中使用即时跟踪记录器 (IFR)


从 Windows 10 开始，可以生成 KMDF 或 UMDF 驱动程序，以便它通过 Windows 软件跟踪预处理获取其他驱动程序调试信息。 此功能称为即时 Trace 录像机 (IFR) ，可从 KMDF 版本1.15 和 UMDF 版本2.15 开始使用。

即时跟踪记录器是 [WPP 软件跟踪](../devtest/wpp-software-tracing.md)的扩展。 与 WPP 跟踪不同，即时跟踪记录器在没有附加跟踪使用者的情况下继续运行。 框架将消息写入循环缓冲区，驱动程序还可以添加自己的消息。 每个驱动程序都有自己的日志，因此与驱动程序相关联的多个设备共享一个日志。

日志存储在不可分页的内存中，因此它们在系统崩溃后是可恢复的。 此外，小型转储文件中还包含即时跟踪记录器日志。

**如何启用即时 Trace 记录器并从驱动程序发送消息**

1.  在 Microsoft Visual Studio 中，执行以下操作：

    -   打开驱动程序项目的属性页。 在“解决方案资源管理器”中右键单击驱动程序项目，并选择“属性”  。 在驱动程序的属性页中，单击 " **配置属性**"，然后单击 " **Wpp 跟踪**"。 在 " **常规** " 菜单上，将 " **运行 WPP 跟踪** " 设置为 **"是"**。

    -   导航到 " **属性"- &gt; Wpp "跟踪- &gt; 函数和宏选项** "，然后选择 " **启用 Wpp 记录器**"。

    -   在同一个菜单中，将 " **扫描配置数据** " 设置为包含跟踪信息的文件，例如 "trace"。

2.  在调用 WPP 宏的每个源文件中，添加标识 [跟踪消息标头](../devtest/trace-message-header-file.md)的 **\# include** 指令 (TMH) 文件。 文件名必须具有 tmh 格式的 &lt; *驱动程序* &gt; **.tmh** 名称。

    例如，如果驱动程序包含两个源文件（称为 *mydriver1.inf* 和 *mydriver2.inf 会被*），则 *mydriver1.inf* 必须包含：

    **\#包括 "Mydriver1.inf. tmh"**

    和 *mydriver2.inf 会被* 必须包含：

    **\#包括 "Mydriver2.inf 会被. tmh"**

    在 Visual Studio 中生成驱动程序时，WPP 预处理器会生成。*tmh* 文件。

3.  在标头文件中定义 [WPP \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 宏。 此宏为驱动程序的跟踪消息定义 GUID 和 [跟踪标志](../devtest/trace-flags.md) 。

    Osrusbfx2 driver 示例定义了 Trace .h 头文件中的单个控件 GUID 和七个跟踪标记，如以下示例中所示：

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

    -   **OsrUsbFxTraceGuid** 是 {D23A0C5A-D307-4F0E-AE8E-E2A355AD5DAB} GUID 的友好名称。
    -   跟踪标记用于区分在驱动程序处理不同类型的 i/o 请求时生成的跟踪消息。

4.  驱动程序 (KMDF 和 UMDF 2) 必须使用驱动程序对象和注册表路径 [**\_ \_ 为 Kernel-Mode 驱动程序调用 WPP INIT 跟踪**](/previous-versions/windows/hardware/drivers/ff556193(v=vs.85)) ，通常来自 [**DriverEntry**](./driverentry-for-kmdf-drivers.md)：

    ```cpp
    WPP_INIT_TRACING( DriverObject, RegistryPath );
    ```

    若要停用跟踪，KMDF 和 UMDF 2 驱动程序都调用 [*EvtCleanupCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)或 [*EvtDriverUnload*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)中 [**\_ Kernel-Mode 驱动程序的 WPP 清除**](/previous-versions/windows/hardware/drivers/ff556183(v=vs.85))：

    ```cpp
    WPP_CLEANUP( WdfDriverWdmGetDriverObject( Driver ));
    ```

    [**WPP \_ 清除**](/previous-versions/windows/hardware/drivers/ff556183(v=vs.85))宏采用类型为 PDRIVER 的参数 \_ ，因此，如果驱动程序的 [**DriverEntry**](./driverentry-for-kmdf-drivers.md)失败，则可以跳过调用 [**WdfDriverWdmGetDriverObject**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriverwdmgetdriverobject) ，而使用指向 WDM 驱动程序对象的指针调用 **WPP \_ 清理**。

    从 UMDF 版本2.15 开始，UMDF 驱动程序使用这些宏的内核模式签名来初始化和清理跟踪。 这意味着，对于 KMDF 和 UMDF，调用看起来相同。

5.  使用驱动程序中的 [**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)) 宏或宏的 [自定义版本](../devtest/can-i-customize-dotracemessage-.md) 来创建跟踪消息。

    下面的示例演示 Osrusbfx2 驱动程序如何在专门用于处理读取请求的代码部分中使用其 **TraceEvents** 函数：

    ```cpp
    if (Length > TEST_BOARD_TRANSFER_BUFFER_SIZE) {
        TraceEvents(TRACE_LEVEL_ERROR,
                    DBG_READ,
                    "Transfer exceeds %d\n",
                    TEST_BOARD_TRANSFER_BUFFER_SIZE);
     
        status = STATUS_INVALID_PARAMETER;
    }
    ```

    如果跟踪控制器启用 **跟踪 \_ 级别 \_ 错误** 级别和 **DBG \_ 读取** 跟踪标志，则对 **TraceEvents** 的调用会生成跟踪消息。 该消息包含驱动程序定义的常量 **测试 \_ 板 \_ 传输 \_ 缓冲区 \_ 大小** 的值。

6.  若要更改驱动程序日志使用的循环缓冲区大小，请在以下注册表位置中修改 **LogPages** 注册表值：

    <a href="" id="for-umdf-"></a>对于 UMDF：  

    **软件 \\ Microsoft \\ Windows NT \\ CurrentVersion \\ WUDF \\ Services \\ &lt; YourDriver &gt; \\ 参数 \\ Wdf**

    <a href="" id="for-kmdf-"></a>对于 KMDF：  

    **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Services \\ &lt; YourDriver &gt; \\ 参数 \\ Wdf**

    这是类型为 **REG \_ DWORD** 的值，包含分配的日志缓冲区大小（以页为限）。 有效值介于0x1 和0x10 之间。

**对于 KMDF 驱动程序**

1.  通过在调试器中键入 **load rcdrkd.dll** 来加载 RCDRKD 命令。
2.  使用 [**！ wdfkd wdfldr**](../debugger/-wdfkd-wdfldr.md) 扩展显示有关当前动态绑定到 Windows 驱动程序框架的驱动程序的信息， (WDF) 。
3.  使用 [**！ rcdrlogdump**](../debugger/-rcdrkd-rcdrlogdump.md) 和 [**rcdrcrashdump rcdrkd**](../debugger/-rcdrkd-rcdrcrashdump.md) 查看驱动程序提供的消息 rcdrkd。
4.  使用 [**！ wdfkd; wdflogdump**](../debugger/-wdfkd-wdflogdump.md) 或 [**！ wdfkd**](../debugger/-wdfkd-wdfcrashdump.md) 查看框架提供的消息。

**UMDF 驱动程序的实时调试**

1.  使用 [**！ wdfkd wdfldr**](../debugger/-wdfkd-wdfldr.md) 扩展显示有关当前动态绑定到 WDF 的驱动程序的信息。 查找用户模式驱动程序。 输入关联的主机进程。
2.  键入 **！ wdfkd. wdflogdump** *&lt;YourDriverName.dll&gt; &lt; 标志 &gt;* ，其中 *&lt; 标志 &gt;* 为：

    -   0x1 –合并的框架和驱动程序日志
    -   0x2 –驱动程序日志
    -   0x3-框架日志

    如果指定的驱动程序没有驱动程序日志，则该扩展只显示框架日志。

**在 UMDF 驱动程序崩溃后查看即时 Trace 录像机日志**

1. 在 WinDbg 中，选择 " **文件"-" &gt; 打开故障转储**"，然后指定要调试的小型转储文件。
2. 键入 [**！ wdfkd. wdfcrashdump *&lt;YourDriverName.dll&gt; &lt; driver host &gt; &lt; 选项 &gt; 的进程 ID***](../debugger/-wdfkd-wdfcrashdump.md)，其中 *&lt; Option &gt;* 是：

   -   0x1 –合并的框架和驱动程序日志
   -   0x2 –驱动程序日志
   -   0x3-框架日志

   如果未指定驱动程序， [**！ wdfcrashdump**](../debugger/-wdfkd-wdfcrashdump.md) 将显示所有驱动程序的信息。 如果未指定宿主进程，并且只有一个进程，则扩展使用单个主机进程。 如果未指定宿主进程，并且有多个进程，则扩展会列出活动的主机进程。

   如果存储在小型转储中的日志信息与输入的名称不匹配，则小型转储不包含驱动程序的日志。

有关将跟踪消息添加到驱动程序的详细信息，请参阅向 [驱动程序添加 WPP 宏](../devtest/adding-wpp-macros-to-a-trace-provider.md)。

## <a name="related-topics"></a>相关主题


[如何启用对 UMDF 驱动程序的调试](enabling-a-debugger.md)

[RCDRKD 扩展](../debugger/rcdrkd-extensions.md)

[使用框架的事件记录器](using-the-framework-s-event-logger.md)

[在 UMDF 驱动程序中使用 WPP 软件跟踪](using-wpp-software-tracing-in-umdf-drivers.md)

 

