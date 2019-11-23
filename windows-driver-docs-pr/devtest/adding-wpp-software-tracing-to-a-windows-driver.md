---
title: 将 WPP 软件跟踪添加到 Windows 驱动程序
description: 若要在跟踪提供程序中（如内核模式驱动程序或用户模式应用程序）使用 WPP 软件跟踪，需要添加代码（或检测）驱动程序源文件并修改驱动程序项目。 本部分将介绍这些步骤。
ms.assetid: 487BA8AA-950A-4F3C-9E3E-EBE1DA35D4B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db2e8fadc5ae9983cd2bd40b8a1215a6812e8355
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840303"
---
# <a name="adding-wpp-software-tracing-to-a-windows-driver"></a>将 WPP 软件跟踪添加到 Windows 驱动程序

若要在跟踪提供程序中（如内核模式驱动程序或用户模式应用程序）使用 WPP 软件跟踪，需要添加代码（或*检测*）驱动程序源文件并修改驱动程序项目。 本部分将介绍这些步骤。

**提示** 向驱动程序添加 WPP 跟踪的最简单方法是在 Visual Studio 中使用 KMDF 或 UMDF 驱动程序模板之一。 如果使用模板，则需要添加的很多代码已经完成。 在 Visual Studio 中，单击 "**文件" &gt; 新建 &gt; 项目**"，然后选择" Windows 驱动程序（用户模式或内核模式） WDF 项目 "。 WPP 宏在作为项目的一部分包含的 Trace .h 头文件中定义。 如果你使用其中一个模板，则可以跳到[步骤 5](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)。 

-   [步骤1：定义控件 GUID 和跟踪标志](#step-1-define-the-control-guid-and-trace-flags)
-   [步骤2：选择要使用的跟踪消息函数并为这些函数定义 WPP 宏](#step-2-choose-which-trace-message-functions-you-intend-to-use-and-define-the-wpp-macros-for-those-functions)
-   [步骤3：在 C 或C++源文件中包含关联的跟踪头文件（.h 和 tmh）](#step-3-include-the-associated-trace-header-files-h-and-tmh-in-your-c-or-c-source-files)
-   [步骤4：将宏添加到相应的回调函数以初始化和清除 WPP](#step-4-add-macros-to-the-appropriate-callback-functions-to-initialize-and-clean-up-wpp)
-   [步骤5：检测驱动程序代码以在适当的点生成跟踪消息](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)
-   [步骤6：修改 Visual Studio 项目以运行 WPP 预处理器并构建解决方案](#step-6-modify-the-visual-studio-project-to-run-the-wpp-preprocessor-and-build-the-solution)
-   [步骤7：启动跟踪会话以捕获和验证跟踪消息](#step-7-start-a-trace-session-to-capture-and-verify-your-trace-messages)

## <a name="step-1-define-the-control-guid-and-trace-flags"></a>步骤1：定义控件 GUID 和跟踪标志

必须对每个跟踪提供程序（如驱动程序或用户模式应用）进行唯一定义。 为此，可以添加[WPP\_控件\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))宏，用于定义控件 GUID、标识符和跟踪标志。 这样就可以确定并控制要跟踪的时间和内容。 虽然每个驱动程序通常都有一个单独的控件 GUID，但驱动程序可以有多个控制 guid，或多个驱动程序可以共享一个控制 GUID。

为方便起见，" [WPP\_控件\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) " 宏通常在公共头文件中定义。 必须在要检测跟踪的任何源文件中包含头文件（\#包含）。

**若要向驱动程序添加 WPP\_控件\_GUID 宏：**

1.  将新C++的标头文件添加到可用于定义 WPP 跟踪宏的 Visual Studio 项目中。 例如，在解决方案资源管理器中右键单击该驱动程序，然后单击 "**添加 &gt; 新项**"。 保存该文件（例如，Trace .h）。

2.  添加[WPP\_控件\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))宏指定跟踪提供程序的友好名称，定义控件 GUID，并定义可用于限定特定跟踪消息的跟踪标志。

    [WPP\_控件\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))宏具有以下语法：

    **WPP\_控件\_GUID 的语法**

    ```ManagedCPlusPlus
    #define WPP_CONTROL_GUIDS \
        WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
            WPP_DEFINE_BIT(NameOfTraceFlag1)  \
            WPP_DEFINE_BIT(NameOfTraceFlag2)  \
            .............................   \
            .............................   \
            WPP_DEFINE_BIT(NameOfTraceFlag31) 
    ```

    例如，下面的代码使用 myDriverTraceGuid 作为*GUIDFriendlyName*。 请注意， *ControlGUID*的格式与32位十六进制 GUID 标准形式的格式略有不同。 *ControlGUID*有五个字段，但它们之间用逗号分隔，并用括号括起来，而不是常用的连字符和大括号。 例如，指定（ **（84bdb2e9，829e，41b3，b891，02f454bc2bd7）** ，而不是 {84bdb2e9-829e-41b3-b891-02f454bc2bd7}。

    **WPP\_控件\_GUID 语句的示例**

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

    **提示** 可以将此代码片段复制到头文件中。 确保更改控件 GUID 和友好名称。 可以使用 Guidgen.exe 生成控件 GUID。 Guidgen.exe 包含在 Visual Studio 中（**Tools &gt; 创建 GUID**）。 你还可以使用 Uuidgen.exe 工具，该工具可从 Visual Studio 命令提示符窗口（键入**uuigen/？** 有关详细信息）。



3.  定义跟踪提供程序的[跟踪标志](trace-flags.md)。

    WPP\_定义 WPP\_控件\_位元素\_GUID 宏为跟踪提供程序定义跟踪标志。 通常，标志表示越来越详细的报表级别，但您可以将标志用作生成跟踪消息的条件。 在 WPP\_控件\_GUID 示例中，WPP\_定义\_位定义四个跟踪标志（MYDRIVER\_所有\_的信息、跟踪\_驱动程序、跟踪\_设备和跟踪\_队列）。

    最多可以定义31个跟踪标志。 WPP 按它们出现的顺序向元素分配位值，例如，位0（0x1）、bit 1 （0x2）、bit 2 （0x4）、bit 3 （0x8）等。 将跟踪消息函数添加到源代码时，可以使用跟踪标志（[步骤5：检测驱动程序代码以在适当的点生成跟踪消息](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)中所述）。

    **注意** 使用跟踪标志，可以控制何时跟踪特定组件（例如，特定 i/o 请求或设备或驱动程序对象的活动）。 将跟踪标志添加到跟踪消息语句（例如 `DoTraceMessage (TRACE_DRIVER, "Hello World!\n")`。 当你使用跟踪控制器（如[Tracelog](tracelog.md)）创建跟踪会话时，你可以指定 **-标志**选项以用于该会话中的跟踪提供程序，在本例中，标志为位1（0x1），这对应于跟踪\_驱动程序标志。 启动跟踪会话时，所有指定该跟踪标志的跟踪消息都将写入日志。



## <a name="step-2-choose-which-trace-message-functions-you-intend-to-use-and-define-the-wpp-macros-for-those-functions"></a>步骤2：选择要使用的跟踪消息函数并为这些函数定义 WPP 宏


与调试打印功能类似，trace 消息函数是添加到代码中以写入跟踪消息的函数（或宏）。

**选择跟踪消息函数**

1.  默认跟踪消息函数为[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))宏。 如果使用默认函数，则可以使用提供程序的[跟踪标志](trace-level.md)值控制何时生成消息。 跟踪标志值是在步骤1中创建控件 GUID 时定义的标志。 如果你使用**DoTraceMessage**，则已为你定义默认的 WPP 宏\_（\_启用和 WPP\_级别\_记录器）的默认 WPP 宏，因此你可以跳过此步骤的其余部分并转到[步骤 5](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)。

2.  如果你使用的是 KMDF 或 UMDF 模板之一，则已定义**TraceEvents**函数和必要的 WPP 宏来启用该函数，因此你可以跳到[步骤 5](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)。

3.  如果要创建自己的跟踪消息函数或转换现有的调试打印功能，请继续执行此步骤的其余部分。

**创建或自定义跟踪消息函数**

1.  如果使用的是自定义跟踪消息函数，或想要转换调试打印功能（例如， [**KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)）以生成跟踪消息，则需要定义 WPP 宏，用于在跟踪提供程序中标识和启用跟踪消息函数。 将这些宏放在已添加到项目的 Trace .h 头文件中。

2.  定义 WPP 宏以启用 trace 函数。

    你使用的每个跟踪消息函数都必须具有相应的宏对。 这些宏标识跟踪提供程序并指定生成消息的条件。 通常，您可以定义一对宏、 **wpp\_ *&lt;条件&gt;* \_记录器**和**wpp\_&lt;&gt;\_\_启用的默认 WPP *\_*** \_\_

你使用的每个跟踪消息函数都必须具有相应的宏对。 这些宏标识跟踪提供程序并指定生成消息的条件。 通常，您可以定义一对宏、 **wpp\_ *&lt;条件&gt;* \_记录器**和**wpp\_&lt;&gt;\_\_启用的默认 WPP *\_*** \_\_

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
<td align="left"><p>用于查找与提供程序关联的跟踪会话并返回会话的句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="WPP_CONDITIONS_ENABLED"></span><span id="wpp_conditions_enabled"></span><strong>WPP</em><em>条件</em>_ENABLED</strong></p></td>
<td align="left"><p>用于确定是否使用指定的条件启用了日志记录。</p></td>
</tr>
</tbody>
</table>



对于您定义的 WPP 宏，*条件*表示跟踪消息函数支持的条件，这些条件按照它们在函数的参数列表中的显示顺序，用下划线分隔。 例如，默认跟踪消息函数[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))仅支持[跟踪标志](trace-level.md)作为条件，因此宏名称中只有一个参数（\_启用了 WPP\_级别）。

**注意** 遗憾的是，默认宏的名称（WPP\_级别\_ENABLED 和 WPP\_级别\_记录器）似乎指出了[跟踪级别](trace-level.md)参数，但实际引用的是跟踪标志。



如果使用自定义跟踪消息函数，则可以设置其他限定符，例如[跟踪级别](trace-level.md)。 跟踪级别是在 Evntrace 文件中定义的，跟踪级别提供了一种将跟踪消息归类为错误、警告和信息性消息的简便方法。

例如，可以将以下代码片段添加到已添加到项目中的头文件。 下面的代码定义跟踪消息函数的自定义 WPP 宏，该函数支持[跟踪级别](trace-level.md)和跟踪标志参数作为生成跟踪消息的条件。 如果为指定的标志值启用了日志记录，并且已启用的级别值大于或等于跟踪消息函数调用中使用的级别参数，则**WPP\_\_级别\_启用**的宏将返回 TRUE。

```ManagedCPlusPlus
#define WPP_LEVEL_FLAGS_LOGGER(lvl,flags) \
           WPP_LEVEL_LOGGER(flags)

#define WPP_LEVEL_FLAGS_ENABLED(lvl, flags) \
           (WPP_LEVEL_ENABLED(flags) && WPP_CONTROL(WPP_BIT_ ## flags).Level >= lvl)
```

接下来，需要在 WPP 配置块中指定自定义跟踪函数（**开始\_wpp config**并**结束\_wpp**）。例如，如果在 VISUAL Studio 中使用 UMDF 或 KMDF 驱动程序项目模板，则该模板将为名为**TraceEvents**的自定义跟踪消息函数定义 WPP 宏。 **TraceEvents**宏函数使用[跟踪级别](trace-level.md)和跟踪标志作为生成消息的条件。 如果在 Trace .h 头文件中定义了**WPP\_级别\_标志\_启用**的宏，则可以添加以下宏定义。

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

您还可以将现有的调试 print 语句转换为跟踪消息语句，方法是在 WPP 配置块中添加类似的**FUNC**声明。 例如，下面的示例添加代码来转换现有的[**KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)语句。 **FUNC**声明还全局定义**KdPrint**以使用指定的跟踪级别并标记 {LEVEL = TRACE\_LEVEL\_信息，FLAGS = trace\_DRIVER}。 调试打印语句将发送到跟踪日志，而不是将输出发送到调试器。

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

**注意** 如果要将[**KdPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)转换为跟踪消息函数，则需要执行一些额外的步骤。 与[**KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)相比， **KdPrintEx**函数采用两个附加参数。 若要转换**KdPrintEx**函数，需要定义一个 WPP\_为该*组件***定义\_位**，  ***&lt;* \_** 并将&gt;记录器和 WPP\_\_&lt;&gt;\_的宏。 **KdPrintEx**的第二个参数指定的级别与[跟踪级别](trace-level.md)值相似，因此你不一定需要重新定义它们。



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

## <a name="step-3-include-the-associated-trace-header-files-h-and-tmh-in-your-c-or-c-source-files"></a>步骤3：在 C 或C++源文件中包含关联的跟踪头文件（.h 和 tmh）


如果在标头文件（例如，trace .h）中为驱动程序定义了控件 GUID 和跟踪标志，则需要在要初始化和卸载 WPP （步骤4）或调用跟踪消息函数的源文件中包含标头文件。

此外，还需要为[跟踪消息头文件](trace-message-header-file.md)（. tmh）添加 **\#包含**语句。 生成驱动程序或应用程序时，WPP 预处理器将为包含跟踪消息函数的每个源文件生成跟踪消息头文件（. tmh）。

```ManagedCPlusPlus
/* -- driver.c  - include the *.tmh file that is generated by WPP --*/

#include "trace.h"     /* file that defines WPP_CONFIG_GUIDS and trace flags */
#include "driver.tmh"  /* this file is auto-generated */
```

## <a name="step-4-add-macros-to-the-appropriate-callback-functions-to-initialize-and-clean-up-wpp"></a>步骤4：将宏添加到相应的回调函数以初始化和清除 WPP


**初始化驱动程序条目的 WPP**

-   向内核模式驱动程序或 UMDF 2.0 驱动程序的*DriverEntry*例程添加[WPP\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))宏，或添加到用户模式驱动程序（UMDF 1.x）或应用程序的*DLLMain*例程。

**清理驱动程序退出的 WPP 资源**

-   向内核模式驱动程序或 UMDF 2.0 驱动程序的驱动程序卸载例程（例如*DriverContextCleanup*或*DriverUnload*）添加[WPP\_清理](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))宏。

    对于用户模式驱动程序（UMDF 1.x）或应用程序，将[WPP\_清理](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))宏添加到*DLLMain*例程。

    还应向*DriverEntry*例程添加[WPP\_清理](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))宏，以防*DriverEntry*失败。 例如，如果*DriverEntry*失败，则不会调用驱动程序卸载例程。 在以下示例中，请参阅对[**WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)的调用。

使用 WPP 的内核模式驱动程序的示例\_INIT\_跟踪和 WPP\_在*DriverEntry*中清除

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

使用 WPP\_在 DriverContextCleanup 中进行清除的内核模式驱动程序的示例

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

使用 WPP 的 UMDF 2.0 驱动程序的示例\_INIT\_DriverEntry 中的跟踪

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

UMDF 1.0 驱动程序的示例使用 WPP\_INIT\_跟踪和 WPP\_清理 DLLMain 中的宏

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

## <a name="step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points"></a>步骤5：检测驱动程序代码以在适当的点生成跟踪消息


您可以使用所选的任何跟踪消息函数（前提是跟踪消息函数、跟踪标志和级别均已正确定义）。 默认跟踪消息函数为[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))宏。 您可以将该宏添加到您的代码中，以便将消息写入日志文件。 下表列出了一些预定义的跟踪消息函数以及可用于创建跟踪消息的调试打印功能。

<table>
<colgroup>
<col width="50%" />

<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">跟踪消息函数示例</th>
<th align="left">何时使用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))"><strong>DoTraceMessage</strong></a></td>
<td align="left"><p>这是默认的跟踪消息函数。 使用<a href="https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))"><strong>DoTraceMessage</strong></a>的优点是已为你定义了该函数。 您可以使用在 WPP_CONFIG_GUIDS 宏中指定的跟踪标志。 使用<strong>DoTraceMessage</strong>的缺点是，该函数只采用一个条件参数，即跟踪标志。 如果希望使用跟踪级别，以只记录错误或警告消息，则可以使用<strong>DoDebugTrace</strong>宏，或使用<strong>TraceEvents</strong>，后者使用跟踪标志和跟踪级别。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>TraceEvents</strong></td>
<td align="left"><p>如果使用 Visual Studio 中的 WDF 模板创建驱动程序，这是默认的跟踪消息函数。 使用<strong>TraceEvents</strong>的优点是已为你定义跟踪消息函数、跟踪标志和<a href="trace-level.md" data-raw-source="[Trace Level](trace-level.md)">跟踪级别</a>。 此外，这些模板还包括检测功能，用于在函数进入和退出时将消息写入日志文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint" data-raw-source="[&lt;strong&gt;KdPrint&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)"><strong>KdPrint</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex" data-raw-source="[&lt;strong&gt;KdPrintEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)"><strong>KdPrintEx</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint" data-raw-source="[&lt;strong&gt;DbgPrint&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint)"><strong>DbgPrint</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex" data-raw-source="[&lt;strong&gt;DbgPrintEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex)"><strong>DbgPrintEx</strong></a></td>
<td align="left"><p>使用调试打印功能的优点是不需要修改现有的调试打印语句。 您可以轻松地从查看调试器中的消息进行切换，以便在文件中记录跟踪消息。 如果自定义跟踪消息函数以包括其中一个调试打印功能，则无需执行任何其他操作。 使用 Logman 或<a href="tracelog.md" data-raw-source="[Tracelog](tracelog.md)">Tracelog</a>或其他跟踪控制器创建跟踪会话时，只需为提供程序指定标志和级别。 任何满足指定条件的调试 print 语句将打印到日志中。</p></td>
</tr>
</tbody>
</table>



<span id="using_dotracemessage"></span><span id="USING_DOTRACEMESSAGE"></span>

**使用 DoTraceMessage 语句**

1.  将[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))宏添加到您的代码中，就像调试打印例程一样。 **DoTraceMessage**宏使用3个参数：标志级别（*TraceFlagName*），它定义跟踪消息写入时的条件、*消息*字符串和可选的变量列表。

    ```
    DoTraceMessage(TraceFlagName, Message, [VariableList... ]
    ```

    例如，当为跟踪会话启用了\_控件\_GUID 中定义的跟踪\_驱动程序标志时，以下[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))语句将写入包含**DoTraceMessage**语句的函数的名称。

    ```ManagedCPlusPlus
         DoTraceMessage( TRACE_DRIVER, "\nEntering %!FUNC!" );

    ```

    该示例为当前正在执行的函数（% FUNC！）的提供了预定义的字符串。 有关 WPP 定义格式规范字符串的详细信息，请参阅[什么是 wpp 扩展格式规范字符串？](what-are-the-wpp-extended-format-specification-strings-.md)

2.  若要生成跟踪消息，请使用 Logman 或[Tracelog](tracelog.md)为跟踪提供程序创建跟踪会话，并指定一个跟踪标志，该标志将\_驱动程序标志（bit 1，0x2）来设置跟踪。

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

<span id="using_traceevents"></span><span id="USING_TRACEEVENTS"></span>如果使用的是 Visual Studio 中的 Windows 驱动程序模板，则在 TraceEvents 头文件中定义了宏。

**使用 TraceEvents 语句**

1.  将**TraceEvents**宏添加到您的代码中，就像调试打印例程一样。 **TraceEvents**宏采用以下参数：跟踪级别（*level*）和跟踪标志（*标志*），用于定义写入跟踪消息时的条件、*消息*字符串和可选变量列表。

    ```
    TraceEvents(Level, Flags, Message, [VariableList... ]
    ```

    例如，以下**TraceEvents**语句在满足[跟踪级别](trace-level.md)和跟踪标志参数中指定的条件时写入包含**TraceEvents**语句的函数的名称。 跟踪级别是一个整数值;将跟踪为跟踪会话指定的跟踪级别下或之下的任何内容。 跟踪\_级别\_信息是在 Evntrace 中定义的，其值为4。 跟踪\_驱动程序标志（bit 1，0x2）是在 WPP\_控件\_GUID 中定义的。 如果为跟踪会话设置了此跟踪\_驱动程序位，并且跟踪级别为4或更大，则**TraceEvents**将写入跟踪消息。

    ```ManagedCPlusPlus
            TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    ```

    该示例为当前正在执行的函数（% FUNC！）的提供了预定义的字符串。 有关 WPP 定义格式规范字符串的详细信息，请参阅[什么是 wpp 扩展格式规范字符串？](what-are-the-wpp-extended-format-specification-strings-.md)

2.  若要生成跟踪消息，请使用 Logman 或[Tracelog](tracelog.md)为跟踪提供程序创建跟踪会话。 指定跟踪级别以跟踪\_级别\_信息（4）或更高级别，并指定设置跟踪\_驱动程序位（bit 1，0x2）的跟踪级别。

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

## <a name="step-6-modify-the-visual-studio-project-to-run-the-wpp-preprocessor-and-build-the-solution"></a>步骤6：修改 Visual Studio 项目以运行 WPP 预处理器并构建解决方案


WDK 为[WPP 预处理器](wpp-preprocessor.md)提供支持，以便你可以使用 Visual Studio 和 MSBuild 环境运行预处理器。

**运行 WPP 预处理器**

1.  在解决方案资源管理器中右键单击驱动程序项目，然后单击 "**属性"。**
2.  在项目属性页中，单击 "**配置属性**"，然后单击 " **WPP 跟踪**"。
3.  在 "**常规**" 下，将 "**运行 WPP** " 选项设置为 **"是"** 。
4.  在 "**命令行**" 下，添加用于自定义跟踪行为的任何其他选项。 有关可添加内容的详细信息，请参阅[WPP 预处理器](wpp-preprocessor.md)。
5.  生成目标配置和平台的项目或解决方案。 请参阅[使用 WDK 构建驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)。

有关生成过程的信息，请参阅[TraceWPP 任务](tracewpp-task.md)和[WDK 和 Visual Studio 生成环境](wdk-and-visual-studio-build-environment.md)。

还可以使用 TraceWPP 工具（TraceWPP）从生成环境运行预处理器。 此工具位于 WDK 的 bin/x86 和 bin/x64 子目录中。

## <a name="step-7-start-a-trace-session-to-capture-and-verify-your-trace-messages"></a>步骤7：启动跟踪会话以捕获和验证跟踪消息


若要验证是否正确设置了 WPP 跟踪，应在测试计算机上安装驱动程序或应用程序，然后创建跟踪会话来捕获跟踪消息。 您可以使用任何跟踪控制器为跟踪提供程序创建跟踪会话，如 Logman、 [Tracelog](tracelog.md)或[TraceView](traceview.md)。 可以将消息写入日志文件，也可以将消息发送到内核调试器。 根据所使用的跟踪消息函数，需要确保指定将生成消息的跟踪标志和跟踪级别。

例如，如果使用 Evntrace 中定义的跟踪级别，并且想要捕获跟踪\_级别\_信息（4）或更高级别，则需要将级别设置为4。 为跟踪会话将级别设置为4时，还将捕获所有信息性（4）、警告（3）、错误（2）和严重（1）消息，假定还满足任何其他条件（如跟踪标志）。

若要验证是否生成了所有消息，只需将跟踪级别和跟踪标志设置为最大值即可生成所有消息。 跟踪标志使用位掩码（ULONG），因此可以设置所有位（例如，0xFFFFFFFF）。 跟踪级别由字节值表示。 例如，如果您使用的是 Logman，则可以指定包含所有级别的0xFF。

实例使用 Logman 启动跟踪会话

```
logman create trace "myWPP_session" -p {11C3AAE4-0D88-41b3-43BD-AC38BF747E19} 0xffffffff 0xff -o c:\DriverTest\TraceFile.etl 

logman start "myWPP_session"

logman stop "myWPP_session"
```

实例使用 TraceLog 启动跟踪会话

```
tracelog -start MyTrace -guid  MyProvider.guid -f d:\traces\testtrace.etl -flag 2 -level 0xFFFF
```

[Tracelog](tracelog.md)命令包括 **-f**参数，用于指定事件跟踪日志文件的名称和位置。 它包括 **-标志**参数，用于指定标志集和**级别**参数以指定级别设置。 您可以省略这些参数，但某些跟踪提供程序不会生成任何跟踪消息，除非您设置了标志或级别。 [跟踪级别](trace-level.md)是在 Evntrace 文件中定义的，跟踪级别提供了一种将跟踪消息归类为关键、错误、警告和信息性消息的简便方法。









