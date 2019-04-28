---
title: 将 WPP 软件跟踪添加到 Windows 驱动程序
description: 若要使用 WPP 软件跟踪在跟踪提供程序，如内核模式驱动程序或用户模式应用程序中，您需要添加代码 （或检测） 驱动程序源文件和修改驱动程序项目。 本部分将介绍这些步骤。
ms.assetid: 487BA8AA-950A-4F3C-9E3E-EBE1DA35D4B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0755dd805032549faaca00bfb4185fac858ffc5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332055"
---
# <a name="adding-wpp-software-tracing-to-a-windows-driver"></a>将 WPP 软件跟踪添加到 Windows 驱动程序

若要使用 WPP 软件跟踪在跟踪提供程序，如内核模式驱动程序或用户模式应用程序中，您需要添加代码 (或*检测*) 驱动程序源文件，并修改驱动程序项目。 本部分将介绍这些步骤。

**提示**将 WPP 跟踪添加到您的驱动程序的最简单方法是在 Visual Studio 中使用 KMDF 或 UMDF 驱动程序模板之一。 如果使用的模板，是已为您完成大部分所需添加的代码。 在 Visual Studio 中，单击**文件&gt;新建&gt;项目**，然后选择 Windows 驱动程序 （用户模式或内核模式） WDF 项目。 包含项目的 Trace.h 标头文件中定义的 WPP 宏。 如果您使用的模板之一，可以跳到[步骤 5](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)。 

-   [步骤 1：定义控件的 GUID 和跟踪标志](#step-1-define-the-control-guid-and-trace-flags)
-   [步骤 2：选择你想要使用并定义这些函数的 WPP 宏的跟踪消息函数](#step-2-choose-which-trace-message-functions-you-intend-to-use-and-define-the-wpp-macros-for-those-functions)
-   [步骤 3：在 C 中包括相关的跟踪标头文件 （.h 和.tmh） 或C++源文件](#step-3-include-the-associated-trace-header-files-h-and-tmh-in-your-c-or-c-source-files)
-   [步骤 4：将宏添加到要初始化和清理 WPP 的相应回调函数](#step-4-add-macros-to-the-appropriate-callback-functions-to-initialize-and-clean-up-wpp)
-   [步骤 5：检测驱动程序代码以生成在适当的位置的跟踪消息](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)
-   [步骤 6：修改 Visual Studio 项目，以运行预处理器 WPP 并生成解决方案](#step-6-modify-the-visual-studio-project-to-run-the-wpp-preprocessor-and-build-the-solution)
-   [步骤 7：启动跟踪会话，以便捕获并验证跟踪消息](#step-7-start-a-trace-session-to-capture-and-verify-your-trace-messages)

## <a name="step-1-define-the-control-guid-and-trace-flags"></a>第 1 步：定义控件的 GUID 和跟踪标志

必须唯一地定义每个跟踪提供程序 （如驱动程序或用户模式应用程序）。 执行此操作通过添加[WPP\_控制\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)宏，用于定义控件 GUID、 标识符和跟踪标志。 这样，以便可以识别并控制何时以及你希望跟踪。 虽然每个驱动程序通常有一个单独的控件的 GUID，驱动程序可以有多个控件的 Guid，或多个驱动程序可以共享一个控件的 GUID。

为方便起见， [WPP\_控制\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)宏通常在常见头文件中定义。 标头文件必须包含 (\#包括) 想要检测的跟踪任何源文件中。

**若要添加 WPP\_控制\_GUID 宏为您的驱动程序：**

1.  添加一个新C++可用于定义 WPP 跟踪宏在 Visual Studio 项目的标头文件。 例如，右键单击解决方案资源管理器中的驱动程序，然后单击**外&gt;新项**。 将该文件 （存 Trace.h，例如)。

2.  添加[WPP\_控制\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)宏来指定跟踪提供程序的友好名称，定义一个控件的 GUID，并定义可用于限定特定跟踪消息的跟踪标志。

    [WPP\_控制\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)宏具有以下语法：

    **语法 WPP\_控制\_GUID**

    ```ManagedCPlusPlus
    #define WPP_CONTROL_GUIDS \
        WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
            WPP_DEFINE_BIT(NameOfTraceFlag1)  \
            WPP_DEFINE_BIT(NameOfTraceFlag2)  \
            .............................   \
            .............................   \
            WPP_DEFINE_BIT(NameOfTraceFlag31) 
    ```

    例如，以下代码使用作为 myDriverTraceGuid *GUIDFriendlyName*。 请注意， *ControlGUID*具有比 32 位十六进制 GUID 的标准格式略有不同的格式。 *ControlGUID*具有五个字段，但它们是以逗号隔开后, 跟括号，而不是常用的连字符和大括号括起来。 例如，指定 (**(84bdb2e9，829e，41b3，b891，02f454bc2bd7)** 而不是 {84bdb2e9-829e-41b3-b891-02f454bc2bd7}。

    **示例 WPP\_控制\_GUID 语句**

    ```ManagedCPlusPlus
    #define WPP_CONTROL_GUIDS                                              \
        WPP_DEFINE_CONTROL_GUID(                                           \
            myDriverTraceGuid, (84bdb2e9,829e,41b3,b891,02f454bc2bd7), \
            WPP_DEFINE_BIT(MYDRIVER_ALL_INFO)        /* bit  0 = 0x00000001 */ \
            WPP_DEFINE_BIT(TRACE_DRIVER)             /* bit  1 = 0x00000002 */ \
            WPP_DEFINE_BIT(TRACE_DEVICE)             /* bit  2 = 0x00000004 */ \
            WPP_DEFINE_BIT(TRACE_QUEUE)              /* bit  3 = 0x00000008 */ \
            )                             
    ```

    **提示**可以将此代码片段复制到的标头文件。 请务必更改控件的 GUID 和友好名称。 GUIDgen.exe 可用于生成控件的 GUID。 Guidgen.exe 是包含在 Visual Studio (**工具&gt;创建 GUID**)。 也可以使用 Uuidgen.exe 工具，它从 Visual Studio 命令提示窗口 (类型**uuigen.exe /？** 有关详细信息）。



3.  定义[跟踪标志](trace-flags.md)跟踪提供程序。

    WPP\_定义\_位元素的 WPP\_控制\_GUID 宏为跟踪提供程序定义的跟踪标志。 通常情况下，标志表示越来越详细的报告级别，但可以为任何喜欢作为条件用于生成跟踪消息的方式使用标志。 在 WPP\_控制\_GUID 的示例中，WPP\_定义\_位定义四个跟踪标志 (MYDRIVER\_所有\_信息、 跟踪\_驱动程序、 跟踪\_设备并跟踪\_队列)。

    您可以定义最多 31 跟踪标志。 WPP 将分配给它们出现的顺序中的元素的位值，位 0 (0x1)、 位 1 (0x2)、 位 2 (0x4)，位 3 (0x8)，依此类推。 在将跟踪消息函数添加到你的源代码使用跟踪标志 (中所述[步骤 5:检测驱动程序代码以生成在适当的位置的跟踪消息](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points))。

    **请注意**使用跟踪标志可以控制何时跟踪特定组件 （例如，特定 I/O 请求或活动的设备或驱动程序的对象）。 将跟踪标志添加到您的跟踪消息语句 (例如， `DoTraceMessage (TRACE_DRIVER, "Hello World!\n")`。 当使用跟踪控制器创建跟踪会话时，如[Tracelog](tracelog.md)，指定 **-标志**选择要在该会话中，在这种情况下，该标志用于跟踪提供程序是第 1 (0x1) 对应的位对跟踪\_驱动程序标志。 在启动跟踪会话时，指定跟踪标志的所有跟踪消息都写入日志。



## <a name="step-2-choose-which-trace-message-functions-you-intend-to-use-and-define-the-wpp-macros-for-those-functions"></a>步骤 2：选择你想要使用并定义这些函数的 WPP 宏的跟踪消息函数


如调试打印的函数，跟踪消息函数是您将添加代码以将跟踪消息写入到函数 （或宏）。

**选择跟踪消息函数**

1.  默认跟踪消息函数是[ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)宏。 如果使用默认函数可控制何时生成消息使用[跟踪标志](trace-level.md)您的提供程序的值。 跟踪标志的值为在步骤 1 中创建控件 GUID 时定义的标志。 如果您使用**DoTraceMessage**，默认 WPP 宏已定义为您 (WPP\_级别\_已启用和 WPP\_级别\_记录器)，因此可以跳过此步骤的其余部分并转到[步骤 5](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)。

2.  如果使用 KMDF 或 UMDF 模板之一**TraceEvents**函数和必要的 WPP 宏已定义要启用该功能，因此你可以跳到[第 5 步](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)。

3.  如果要创建自己的跟踪消息函数，或转换现有调试打印函数，请继续进行此步骤的其余部分。

**创建或自定义跟踪消息函数**

1.  如果你正在使用的自定义跟踪消息功能，或者想要将调试打印功能转换 (例如， [ **KdPrint**](https://msdn.microsoft.com/library/windows/hardware/ff548092)) 若要生成跟踪消息，您需要定义用于标识和启用 WPP 宏跟踪提供程序中的跟踪消息函数。 Trace.h 标头文件添加到你的项目中放入这些宏。

2.  定义 WPP 宏，以启用跟踪功能。

    使用每个跟踪消息函数必须具有相对应的宏对。 这些宏标识跟踪提供程序，并指定生成消息的条件。 通常定义的宏，对**WPP\_*&lt;条件&gt;*\_记录器**并**WPP\_ *&lt;条件&gt;*\_已启用**方面默认 WPP\_级别\_已启用和 WPP\_级别\_记录器的宏。

使用每个跟踪消息函数必须具有相对应的宏对。 这些宏标识跟踪提供程序，并指定生成消息的条件。 通常定义的宏，对**WPP\_*&lt;条件&gt;*\_记录器**并**WPP\_ *&lt;条件&gt;*\_已启用**方面默认 WPP\_级别\_已启用和 WPP\_级别\_记录器的宏。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="WPP_CONDITIONS_LOGGER"></span><span id="wpp_conditions_logger"></span><strong>WPP_<em>条件</em><em>记录器</strong></p></td>
<td align="left"><p>用于查找跟踪会话与提供程序关联，并返回到该会话的句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="WPP_CONDITIONS_ENABLED"></span><span id="wpp_conditions_enabled"></span><strong>WPP</em><em>CONDITIONS</em>_ENABLED</strong></p></td>
<td align="left"><p>用于确定是否使用指定的条件启用日志记录。</p></td>
</tr>
</tbody>
</table>



定义，WPP 宏*条件*表示跟踪消息函数支持，以下划线分隔的函数的参数列表中的显示顺序的条件。 例如，默认跟踪消息函数[ **DoTraceMessage**](https://msdn.microsoft.com/library/windows/hardware/ff544918)，仅支持[跟踪标志](trace-level.md)作为条件，因此，只有一个参数在宏名称中 (WPP\_级别\_已启用)。

**请注意**遗憾的是，默认宏的名称 (WPP\_级别\_已启用和 WPP\_级别\_记录器) 似乎指出了[跟踪级别](trace-level.md)参数，但它们实际上是指跟踪标志。



如果使用自定义跟踪消息函数，你可以设置额外的限定符，如[跟踪级别](trace-level.md)。 Evntrace.h 文件中定义跟踪级别和跟踪级别提供方便的分类为错误、 警告和信息性消息的跟踪消息。

例如，可以将下面的代码段添加到标头文件添加到你的项目。 下面的代码定义支持的跟踪消息函数的自定义 WPP 宏[跟踪级别](trace-level.md)和作为条件生成跟踪消息的跟踪标志参数。 **WPP\_级别\_标志\_已启用**宏返回 TRUE，如果指定的标志值启用日志记录，并且已启用的级别值是大于或等于级别中使用的参数跟踪消息函数调用。

```ManagedCPlusPlus
#define WPP_LEVEL_FLAGS_LOGGER(lvl,flags) \
           WPP_LEVEL_LOGGER(flags)

#define WPP_LEVEL_FLAGS_ENABLED(lvl, flags) \
           (WPP_LEVEL_ENABLED(flags) && WPP_CONTROL(WPP_BIT_ ## flags).Level >= lvl)
```

接下来，需要在 WPP 配置块中指定的自定义跟踪函数 (**开始\_wpp config**并**最终\_wpp**) 例如，如果该模板用于 UMDF 或 KMDFVisual Studio 中的驱动程序项目模板定义一个名为的自定义跟踪消息函数的 WPP 宏**TraceEvents**。 **TraceEvents**宏函数使用[跟踪级别](trace-level.md)和作为用于生成消息的条件的跟踪标志。 如果已定义**WPP\_级别\_标志\_已启用**宏在 Trace.h 标头文件中，可以添加以下宏定义。

```ManagedCPlusPlus
//
// This comment block is scanned by the trace preprocessor to define the 
// TraceEvents function.
//
// begin_wpp config
// FUNC TraceEvents(LEVEL, FLAGS, MSG, ...);
// end_wpp
//
```

此外可以将现有调试 print 语句转换为跟踪语句通过添加一个类似的消息**FUNC** WPP 配置块中的声明。 例如，下面的示例添加的代码要转换的现有[ **KdPrint** ](https://msdn.microsoft.com/library/windows/hardware/ff548092)语句。 **FUNC**声明全局还定义了**KdPrint**若要使用指定的跟踪级别和标志 {级别 = 跟踪\_级别\_信息、 标志 = 跟踪\_驱动程序}。 而不是将输出发送到调试器，调试 print 语句发送到跟踪日志。

```ManagedCPlusPlus
//
// This comment block is scanned by the trace preprocessor to define the
// TraceEvents function and conversion for KdPrint. Note the double parentheses for the KdPrint message, for compatiblility with the KdPrint function.
//
// begin_wpp config
// FUNC TraceEvents(LEVEL, FLAGS, MSG, ...);
// FUNC KdPrint{LEVEL=TRACE_LEVEL_INFORMATION, FLAGS=TRACE_DRIVER}((MSG, ...));
// end_wpp
//
```

**请注意**如果你想要转换[ **KdPrintEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548100)为跟踪消息函数，需要执行一些额外的步骤。 相比[ **KdPrint**](https://msdn.microsoft.com/library/windows/hardware/ff548092)，则**KdPrintEx**函数采用两个其他参数。 要转换**KdPrintEx**函数，您需要定义**WPP\_定义\_位**有关*ComponentID*，并定义自定义**WPP\_*&lt;条件&gt;*\_记录器**并**WPP\_  *&lt;条件&gt;*\_已启用**宏。 第二个参数**KdPrintEx**指定的级别是类似于[跟踪级别](trace-level.md)值，因此不一定要重新定义它们。



```ManagedCPlusPlus

#define WPP_CONTROL_GUIDS                                              \
    WPP_DEFINE_CONTROL_GUID(\
    myDriverTraceGuid, (11C3AAE4, 0D88, 41b3, 43BD, AC38BF747E19), \    /* change GUID for your provider */
        WPP_DEFINE_BIT(MYDRIVER_ALL_INFO)        /* bit  0 = 0x00000001 */ \
        WPP_DEFINE_BIT(TRACE_DRIVER)             /* bit  1 = 0x00000002 */ \
        WPP_DEFINE_BIT(TRACE_DEVICE)             /* bit  2 = 0x00000004 */ \
        WPP_DEFINE_BIT(TRACE_QUEUE)              /* bit  3 = 0x00000008 */ \
        WPP_DEFINE_BIT(DPFLTR_IHVDRIVER_ID)      /* bit  4 = 0x00000010 */\         /* Added for the ComponentID param of KdPrintEx */
    )

#define WPP_Flags_LEVEL_LOGGER(Flags, level)                                  \
    WPP_LEVEL_LOGGER(Flags)

#define WPP_Flags_LEVEL_ENABLED(Flags, level)                                 \
    (WPP_LEVEL_ENABLED(Flags) && \
    WPP_CONTROL(WPP_BIT_ ## Flags).Level >= level)



//
// This comment block is scanned by the trace preprocessor to convert the KdPrintEx function.
// Note the double parentheses for the KdPrint message, for compatiblility with the KdPrintEx function.
//
// begin_wpp config
// FUNC KdPrintEx((Flags, LEVEL, MSG, ...));   
// end_wpp
//
```

## <a name="step-3-include-the-associated-trace-header-files-h-and-tmh-in-your-c-or-c-source-files"></a>步骤 3:在 C 中包括相关的跟踪标头文件 （.h 和.tmh） 或C++源文件


如果为您的驱动程序标头文件 (例如，trace.h) 中定义的控件 GUID 和跟踪标志，您需要将在其中初始化和卸载 WPP (步骤 4) 或调用跟踪消息的函数在源文件中包含头文件。

此外，您需要添加**\#包括**语句[跟踪消息标头文件](trace-message-header-file.md)(.tmh)。 生成的驱动程序或应用程序时，预处理器 WPP 将为每个源文件，其中包含跟踪消息函数生成跟踪消息标头文件 (.tmh)。

```ManagedCPlusPlus
/* -- driver.c  - include the *.tmh file that is generated by WPP --*/

#include "trace.h"     /* file that defines WPP_CONFIG_GUIDS and trace flags */
#include "driver.tmh"  /* this file is auto-generated */
```

## <a name="step-4-add-macros-to-the-appropriate-callback-functions-to-initialize-and-clean-up-wpp"></a>步骤 4：将宏添加到要初始化和清理 WPP 的相应回调函数


**对驱动程序入口初始化 WPP**

-   添加[WPP\_INIT\_跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556191)到宏*DriverEntry*例程的内核模式驱动程序或 UMDF 2.0 驱动程序，或对*DLLMain*用户模式驱动程序的例程 (UMDF 1.x) 或应用程序。

**若要清理 WPP 资源上驱动程序退出**

-   添加[WPP\_清理](https://msdn.microsoft.com/library/windows/hardware/ff556179)宏为驱动程序卸载例程 (例如， *DriverContextCleanup*或*DriverUnload*) 的内核模式驱动程序或 UMDF 2.0驱动程序。

    用户模式驱动程序 (UMDF 1.x) 或应用程序中，添加[WPP\_清理](https://msdn.microsoft.com/library/windows/hardware/ff556179)到宏*DLLMain*例程。

    您还应添加[WPP\_清理](https://msdn.microsoft.com/library/windows/hardware/ff556179)到宏*DriverEntry*例程中用例*DriverEntry*失败。 例如，如果*DriverEntry*失败，不会调用驱动程序卸载例程。 请参阅在调用[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)在下面的示例。

示例中的内核模式驱动程序使用 WPP\_INIT\_跟踪和 WPP\_中清除*DriverEntry*

```ManagedCPlusPlus

NTSTATUS
DriverEntry(
    _In_ PDRIVER_OBJECT  DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{  

          //  ... 

                //
    // Initialize WPP Tracing in DriverEntry
    //
    WPP_INIT_TRACING( DriverObject, RegistryPath );

                //  ...


 //
    // Create a framework driver object to represent our driver.
    //
    status = WdfDriverCreate(
        DriverObject,
        RegistryPath,
        &attributes, // Driver Object Attributes
        &config,          // Driver Config Info
        WDF_NO_HANDLE // hDriver
        );

    if (!NT_SUCCESS(status)) {

        TraceEvents(TRACE_LEVEL_ERROR, DBG_INIT,
                "WdfDriverCreate failed with status 0x%x\n", status);
        //
        // Cleanup tracing here because DriverContextCleanup will not be called
        // as we have failed to create WDFDRIVER object itself.
        // Please note that if you return failure from DriverEntry after the
        // WDFDRIVER object is created successfully, you don't have to
        // call WPP cleanup because in those cases DriverContextCleanup
        // will be executed when the framework deletes the DriverObject.
        //
        WPP_CLEANUP(DriverObject);

    }

                return status;

}
```

使用 WPP 的内核模式驱动程序的示例\_DriverContextCleanup 中清除

```ManagedCPlusPlus


VOID
DriverContextCleanup(
       PDRIVER_OBJECT DriverObject
       )
{
    // ...

    // Clean up WPP resources on unload
    //
    WPP_CLEANUP(DriverObject);

   // ...

}
```

例如 UMDF 2.0 驱动程序使用 WPP\_INIT\_在 DriverEntry 中进行跟踪

```ManagedCPlusPlus

/
// Driver specific #defines in trace header file (trace.h)
//
#define MYDRIVER_TRACING_ID      L"Microsoft\\UMDF2.0\\UMDF2_0Driver1 V1.0"
```

```ManagedCPlusPlus

 // Initialize WPP Tracing in the DriverEntry routine
 //
    WPP_INIT_TRACING( MYDRIVER_TRACING_ID );
```

WPP UMDF 1.0 驱动程序使用的示例\_INIT\_跟踪和 WPP\_DLLMain 中的清理宏

```ManagedCPlusPlus
/
// Driver specific #defines in trace header file (for example, trace.h)
//
#define MYDRIVER_TRACING_ID      L"Microsoft\\UMDF1.X\\UMDF1_XDriver1"


//
// DLL Entry Point - UMDF 1.0 example in the source file where you implement the DLL exports.
// 

extern "C"
BOOL
WINAPI
DllMain(
    HINSTANCE hInstance,
    DWORD dwReason,
    LPVOID lpReserved
    )
{
    if (dwReason == DLL_PROCESS_ATTACH) {
        WPP_INIT_TRACING(MYDRIVER_TRACING_ID);              // Initialize WPP tracing

        g_hInstance = hInstance;
        DisableThreadLibraryCalls(hInstance);

    } else if (dwReason == DLL_PROCESS_DETACH) {
        WPP_CLEANUP();                                                                                                              // Deactivate and cleanup WPP tracing
    }

    return _AtlModule.DllMain(dwReason, lpReserved);
}
```

## <a name="step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points"></a>步骤 5：检测驱动程序代码以生成在适当的位置的跟踪消息


提供适当地定义函数的跟踪消息、 跟踪标志和级别，可以使用您选择任何跟踪消息函数。 默认跟踪消息函数是[ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)宏。 可以将此宏添加到您的代码以将消息写入到日志文件。 下表列出了一些预定义的跟踪消息函数和调试打印的函数可用于创建跟踪消息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">示例跟踪消息函数</th>
<th align="left">何时使用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff544918" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544918)"><strong>DoTraceMessage</strong></a></td>
<td align="left"><p>这是默认跟踪消息函数。 使用的优点<a href="https://msdn.microsoft.com/library/windows/hardware/ff544918" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544918)"> <strong>DoTraceMessage</strong> </a>是已为用户定义函数。 可以使用在 WPP_CONFIG_GUIDS 宏中指定的跟踪标志。 使用的缺点<strong>DoTraceMessage</strong>，是该函数仅采用一个条件参数，即，跟踪标志。 如果你想要使用的跟踪级别，以记录仅错误或警告消息，则可以使用<strong>DoDebugTrace</strong>宏或使用<strong>TraceEvents</strong>，它使用跟踪标志和跟踪级别。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>TraceEvents</strong></td>
<td align="left"><p>如果您创建 WDF 模板使用 Visual Studio 中的驱动程序，这是默认跟踪消息函数。 使用的优点<strong>TraceEvents</strong>是，跟踪消息函数，跟踪标志，并<a href="trace-level.md" data-raw-source="[Trace Level](trace-level.md)">跟踪级别</a>已为你定义。 此外，模板还包含检测机制来将消息写入到函数入口和退出的日志文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff548092" data-raw-source="[&lt;strong&gt;KdPrint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548092)"><strong>KdPrint</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff548100" data-raw-source="[&lt;strong&gt;KdPrintEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548100)"> <strong>KdPrintEx</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff543632" data-raw-source="[&lt;strong&gt;DbgPrint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543632)"> <strong>DbgPrint</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff543634" data-raw-source="[&lt;strong&gt;DbgPrintEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543634)"> <strong>DbgPrintEx</strong></a></td>
<td align="left"><p>使用调试打印功能的优点是不需要修改现有的调试 print 语句。 您可以轻松地切换到在文件中记录跟踪消息在调试器中查看消息。 如果自定义跟踪消息函数，以包含一个调试打印功能，您不需要执行任何更多的工作。 使用 Logman 创建跟踪会话时或<a href="tracelog.md" data-raw-source="[Tracelog](tracelog.md)">Tracelog</a>，或另一个跟踪控制器，你只需指定标志和级别为您的提供程序。 满足指定的条件的任何调试 print 语句输出到日志中。</p></td>
</tr>
</tbody>
</table>



<span id="using_dotracemessage"></span><span id="USING_DOTRACEMESSAGE"></span>
**使用 DoTraceMessage 语句**

1.  添加[ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)到你的代码像调试打印例程的宏。 **DoTraceMessage**宏有 3 个参数： 标志级别 (*TraceFlagName*)，其定义的条件时写入跟踪消息，*消息*字符串，和可选的变量列表。

    ```
    DoTraceMessage(TraceFlagName, Message, [VariableList... ]
    ```

    例如，以下[ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)语句将包含该函数的名称写入**DoTraceMessage**语句时跟踪\_驱动程序的标志，WPP 中定义\_控制\_GUID，启用跟踪会话。

    ```ManagedCPlusPlus
         DoTraceMessage( TRACE_DRIVER, "\nEntering %!FUNC!" );

    ```

    该示例使用的预定义的字符串的当前执行的函数 （%f u n C ！）。 详细了解 WPP 定义格式规范字符串，请参阅[什么是 WPP 扩展格式规范字符串？](what-are-the-wpp-extended-format-specification-strings-.md)

2.  若要生成的跟踪消息，可为跟踪提供程序，使用 Logman 创建跟踪会话或[Tracelog](tracelog.md)，并指定设置的跟踪的跟踪标志\_驱动程序标志 （位 1、 0x2）。

```ManagedCPlusPlus
//
//  DoTraceMessage examples
// 

     ...

// writes the name of the function that contains the trace statement when the flag, TRACE_DRIVER (bit 1, 0x2), 
// as defined in WPP_CONTROL_GUIDS, is enabled for the trace session.

     DoTraceMessage( TRACE_DRIVER, "\nEntering %!FUNC!" );

     ...

// writes the name of the function, the line number, and the error code 

      DoTraceMessage(
            TRACE_DRIVER,
            "[%s] Failed at %d (error code= %d)\n",
            __FUNCTION__,
            __LINE__,
            dwLastError);
```

<span id="using_traceevents"></span><span id="USING_TRACEEVENTS"></span> 如果在 Visual Studio 中，使用 Windows 驱动程序模板**TraceEvents** Trace.h 标头文件中为你定义宏。

**使用 TraceEvents 语句**

1.  添加**TraceEvents**到你的代码像调试打印例程的宏。 **TraceEvents**宏采用以下参数： 跟踪级别 (*级别*) 和跟踪标志 (*标志*)，其定义的条件跟踪消息时编写的*消息*字符串和可选的变量列表。

    ```
    TraceEvents(Level, Flags, Message, [VariableList... ]
    ```

    例如，以下**TraceEvents**语句将包含该函数的名称写入**TraceEvents**语句中指定条件时[跟踪级别](trace-level.md)并且满足跟踪标志参数。 跟踪级别是一个整数值;任何内容或以下跟踪级别为指定，将跟踪跟踪会话。 跟踪\_级别\_信息在 Evntrace.h 中定义并具有值 4。 跟踪\_驱动程序标志 （位 1、 0x2） 定义在 WPP\_控制\_GUID。 如果此跟踪\_驱动程序位设置为跟踪会话，而跟踪级别为 4 或更高版本**TraceEvents**写入跟踪消息。

    ```ManagedCPlusPlus
            TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    ```

    该示例使用的预定义的字符串的当前执行的函数 （%f u n C ！）。 详细了解 WPP 定义格式规范字符串，请参阅[什么是 WPP 扩展格式规范字符串？](what-are-the-wpp-extended-format-specification-strings-.md)

2.  若要生成的跟踪消息，可为跟踪提供程序，使用 Logman 创建跟踪会话或[Tracelog](tracelog.md)。 指定跟踪级别跟踪\_级别\_信息 (4) 或更高版本，并指定设置的跟踪的跟踪级别\_驱动程序位 （位 1、 0x2）。

```ManagedCPlusPlus
//
//  TraceEvents examples
// 


    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

//


    TraceEvents(TRACE_LEVEL_INFORMATION, DBG_INIT,
                       "OSRUSBFX2 Driver Sample - Driver Framework Edition.\n");

    TraceEvents(TRACE_LEVEL_INFORMATION, DBG_INIT,
                "Built %s %s\n", __DATE__, __TIME__);
```

## <a name="step-6-modify-the-visual-studio-project-to-run-the-wpp-preprocessor-and-build-the-solution"></a>步骤 6：修改 Visual Studio 项目，以运行预处理器 WPP 并生成解决方案


WDK 提供了对支持[WPP 预处理器](wpp-preprocessor.md)，以便可以运行使用 Visual Studio 和 MSBuild 环境预处理器。

**若要运行 WPP 预处理器**

1.  右键单击解决方案资源管理器中的驱动程序项目，然后单击**属性。**
2.  在项目属性页中，单击**配置属性**然后单击**WPP 跟踪**。
3.  下**常规**，请设置**运行 WPP**选项设置为**是**。
4.  下**命令行**，添加自定义跟踪行为的任何其他选项。 有关可以添加的内容的信息，请参见[WPP 预处理器](wpp-preprocessor.md)。
5.  生成项目或解决方案的目标配置和平台。 请参阅[构建的驱动程序有 WDK](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)。

有关生成过程的信息，请参阅[TraceWPP 任务](tracewpp-task.md)并[WDK 和 Visual Studio 构建环境](wdk-and-visual-studio-build-environment.md)。

此外可以通过使用 TraceWPP 工具 (TraceWPP.exe)，从生成环境中运行单独的预处理器。 此工具位于 WDK 的 bin/x86 和 bin/x64 子目录中。

## <a name="step-7-start-a-trace-session-to-capture-and-verify-your-trace-messages"></a>步骤 7：启动跟踪会话，以便捕获并验证跟踪消息


若要验证是否已设置 WPP 正确跟踪，应在测试计算机上安装驱动程序或应用程序，并创建一个跟踪会话，以捕获跟踪消息。 您可以为使用任何跟踪控制器，例如 Logman，向跟踪提供程序创建跟踪会话[Tracelog](tracelog.md)，或[TraceView](traceview.md)。 可以将这些消息写入日志文件或发送到内核调试程序。 根据正在使用的跟踪消息函数，您需要确保指定跟踪标志并将生成消息的跟踪级别。

例如，如果您是 Evntrace.h 中, 使用的跟踪级别定义，并且你想要跟踪内容捕获\_级别\_信息 (4) 或更高版本，您需要将级别设置为 4。 当跟踪会话，所有信息性 (4)，将级别设置为 4 时警告 (3)、 (2)、 错误和严重 (1) 消息将还捕获，假设也满足其他条件，如跟踪标志。

若要验证生成所有消息，你可能只需设置跟踪级别和跟踪标志为最大值，以便在都生成的所有消息。 跟踪标志使用位掩码 (ULONG)，因此您可以将所有位都设置 (例如，0xFFFFFFFF)。 跟踪级别由一个字节值表示。 例如，如果使用 Logman，可以指定为 0xFF 涵盖所有级别。

（示例）启动跟踪会话使用 Logman

```
logman create trace "myWPP_session" -p {11C3AAE4-0D88-41b3-43BD-AC38BF747E19} 0xffffffff 0xff -o c:\DriverTest\TraceFile.etl 

logman start "myWPP_session"

logman stop "myWPP_session"
```

（示例）启动跟踪会话使用跟踪日志

```
tracelog -start MyTrace -guid  MyProvider.guid -f d:\traces\testtrace.etl -flag 2 -level 0xFFFF
```

[Tracelog](tracelog.md)命令包括 **-f**参数指定的名称和事件跟踪日志文件的位置。 它包括 **-标志**参数指定的标志集并 **-级别**参数指定的级别设置。 可以省略这些参数，但除非设置了标志或级别，否则某些跟踪提供程序不生成任何跟踪消息。 [跟踪级别](trace-level.md)Evntrace.h 文件中定义和跟踪级别提供方便的分类为关键的跟踪消息、 错误、 警告和信息性消息。









