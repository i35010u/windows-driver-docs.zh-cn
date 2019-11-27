---
title: 日志记录跟踪的即时跟踪记录器（IFR）
description: 即时 Trace 录像机（IFR）是一种新的跟踪功能，它允许跟踪提供程序（如内核模式驱动程序）使用最小的设置获取跟踪日志，并创建一组内存中缓冲区，其中保留了最新的 WPP 日志消息。
ms.assetid: D11FA28E-3B0C-4D9D-AEDA-8A80DE58091C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3399d177ef7a801f9f81da3849a8d87193a16172
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839262"
---
# <a name="inflight-trace-recorder-ifr-for-logging-traces"></a>日志记录跟踪的即时跟踪记录器（IFR）


**摘要**

-   如何在 Visual Studio 中启用即时 Trace 记录器
-   如何将跟踪消息发送到 WPP 默认日志或自定义日志
-   如何在调试器中查看跟踪消息

**适用对象：**

-   最小 OS：适用于 KMDF 和 WDM 驱动程序开发人员的 Windows 8
-   最低操作系统： Windows 10 for UMDF （2.15）驱动程序开发人员

**重要的 API**

-   [**WppRecorderLogGetDefault**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn895240(v=vs.85))
-   [**WppRecorderLogCreate （仅限内核模式驱动程序）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)
-   [**WppRecorderDumpLiveDriverData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderdumplivedriverdata)

*即时 Trace 录像机（IFR）* 是一种新的跟踪功能，它允许跟踪提供程序（如内核模式驱动程序）使用最小的设置获取跟踪日志，并创建一组内存中缓冲区，其中保留了最新的 WPP 日志消息。

Windows 提供了几种机制，可用于向驱动程序添加跟踪消息，从而帮助你诊断和调试开发期间的驱动程序中的问题。 这种机制是[WPP 软件跟踪](wpp-software-tracing.md)。 它包括一个[WPP 预处理器](wpp-preprocessor.md)，使跟踪提供程序可具有具有更小内存需求量的 printf 样式的跟踪消息。 但是，若要查看跟踪消息的日志，必须启用该提供程序，跟踪控制器（如[TraceView](traceview.md)或[Tracelog](tracelog.md) ）必须停止并启动跟踪会话才能创建日志，然后，使用者（如 TraceView）必须设置格式并显示日志。

Windows 10 引入了一项新功能：利用 WPP 基础结构的 IFR。 如果驱动程序启用 WPP 跟踪和 IFR，则会自动启用跟踪日志记录，并且无需启动或停止跟踪会话即可轻松查看消息。

IFR 从驱动程序的非分页池分配一个内存页（称为*默认日志*）。 日志收集驱动程序发送的跟踪消息，您可以在驱动程序运行时查看内核调试器中的缓冲区输出。 如果发生崩溃，可以在转储中获取最新的跟踪消息。 无需重新构建崩溃即可收集跟踪数据。

默认日志非常有用，因为驱动程序可以使用最小配置来获取跟踪日志。 请注意，驱动程序无法控制默认日志的大小。 由于所有跟踪消息都发送到一个循环缓冲区，因此，最新消息将覆盖以前的消息，而不考虑信息的级别。 可能会错过错误消息，只能看到信息消息。

为了更好地控制日志 bugger，IFR 允许驱动程序创建和管理自定义缓冲区。

**注意** 在此版本的 Windows 中，只有内核模式驱动程序（KMDF 和 WDM）才能创建自定义缓冲区。 UMDF 驱动程序无法创建自定义缓冲区。



-   驱动程序可以出于不同目的创建多个缓冲区，以便详细记录器不会淹没缓冲区。
-   驱动程序可以控制自定义缓冲区的大小和自定义缓冲区的错误分区（稍后讨论）。
-   驱动程序可以为自定义日志指定字符串标识符。 查看跟踪消息时，可以区分不同缓冲区中的消息。
-   由于 IFR 是在 WPP 上构建的，即使为驱动程序启用了 IFR，也可在[TraceView](traceview.md)中查看 WPP 消息。 但是，若要查看这些消息，您必须启用跟踪提供程序并启动会话。

**重要须知**  
IFR 中的消息没有与之相关联的时间戳。

只能在 Windows 调试器中查看跟踪消息。



## <a name="span-idbefore_you_beginspanspan-idbefore_you_beginspanspan-idbefore_you_beginspanbefore-you-begin"></a><span id="Before_you_begin..."></span><span id="before_you_begin..."></span><span id="BEFORE_YOU_BEGIN..."></span>开始之前 。


-   熟悉[wpp 软件跟踪](wpp-software-tracing.md)，例如向[驱动程序添加 wpp 软件跟踪](adding-wpp-software-tracing-to-a-windows-driver.md)，并[声明和调用 WPP 宏](adding-wpp-macros-to-a-trace-provider.md)。
-   阅读此博客文章，了解[如何在驱动程序的公共 PDB 文件中包含和查看 WPP 跟踪消息](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog/archive/2013/06/29/wpp-blog-post.aspx)。
-   研究 toaster 示例。 已对其进行了修改，演示如何启用 IFR 并使用它。 有关详细信息，请参阅[Toaster 示例驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=617723)。

## <a name="span-idenable_wpp_software_tracingspanspan-idenable_wpp_software_tracingspanspan-idenable_wpp_software_tracingspanenable-wpp-software-tracing"></a><span id="Enable_WPP_software_tracing"></span><span id="enable_wpp_software_tracing"></span><span id="ENABLE_WPP_SOFTWARE_TRACING"></span>启用 WPP 软件跟踪


必须先将驱动程序设置为 WPP[跟踪提供程序](trace-provider.md)，然后才能将驱动程序配置为使用 IFR。

-   如果使用 Visual Studio 中提供的 WDF 驱动程序模板创建了驱动程序，则会启用 WPP 跟踪。 查看项目属性中与跟踪相关的设置。

    1.  在 Visual Studio 中，右键单击要在解决方案资源管理器中启用的项目，然后单击 "**属性"。**
    2.  将配置和平台设置为你打算支持的生成目标（例如，所有配置和所有平台）。
    3.  在项目属性页中，选择 "**配置属性**"，然后单击 " **WPP 跟踪**"。
    4.  在 "**常规**" 下，单击 "**运行 Wpp 跟踪**"，从下拉菜单中选择 **"是"** ，然后单击 **"确定"** 。

        ![在 visual studio 中启用 wpp 软件跟踪](images/wpp-enable.png)

    5.  在 "**文件选项**" 下，将 "**扫描配置数据**" 的值设置为包含调试跟踪相关函数定义和宏的跟踪信息文件的名称。 在此示例中，定义位于 node.js 中。

        ![在 visual studio 中启用 wpp 软件跟踪](images/wpp-enable2.png)

-   如果你使用的不是一个 WDF 驱动程序模板，请设置 WPP 软件跟踪。 创建标头文件（类似于使用 WDF 模板提供的 node.js）。 该标头文件包含 WPP 宏（[wpp\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))、 [wpp\_清理](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))）和 wpp 控制标志和跟踪消息语句。 有关说明，请参阅向[Windows 驱动程序添加 WPP 软件跟踪](adding-wpp-software-tracing-to-a-windows-driver.md)。

    请确保执行以下任务：

    -   定义驱动程序的 GUID 作为跟踪提供程序。

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

    -   将跟踪头文件（在此示例中为 Trace）包含在将打印跟踪语句的源文件中。
    -   在包含要打印的跟踪消息的源文件中包括与源文件关联的[跟踪消息格式](trace-message-format-file.md)文件（ *&lt;源文件&gt;* tmh）。
        ```ManagedCPlusPlus
        #include "trace.h"
        //
        // This tmh is generated by the WPP Preprocessor.
        //
        #include "MyDriver.tmh"
        ```

    -   初始化驱动程序的[DriverEntry](28131-driverentry-saving-pointer-to-buffer.md)中的 WPP。
        ```ManagedCPlusPlus
        //
        // WPP Initialization
        //
        WPP_INIT_TRACING(DriverObject, RegistryPath);

        ```

    -   在驱动程序卸载方法中释放 WPP 资源。
        ```ManagedCPlusPlus
        //
        // WPP release resources
        //

        WPP_CLEANUP( DriverObject) );
        ```

## <a name="span-idstep_2spanspan-idstep_2spanenable-ifr"></a><span id="step_2"></span><span id="STEP_2"></span>启用 IFR


向驱动程序添加 WPP 软件跟踪之后，IFR 基础结构已准备就绪。 只需在项目属性中启用该功能。

1.  在 Visual Studio 中，右键单击要在解决方案资源管理器中启用的项目，然后单击 "**属性"。**
2.  将配置和平台设置为你打算支持的生成目标（例如，所有配置和所有平台）。
3.  在项目属性页中，单击 "**配置属性**"，然后单击 " **WPP 跟踪**"。
4.  在 "**函数和宏选项**" 下，单击 "**启用 WPP 记录器**"，从下拉菜单中选择 **"是"** ，然后单击 **"确定"** 。

    这会定义**enable\_WPP\_记录器**编译器标志，还可以为 KMDF 驱动程序设置启用 dll 宏（用于 UMDF 驱动程序的 **--** **公里**）。

    即使启用了 IFR，也仍然可以使用 Windows 驱动程序工具包（WDK）中包含的工具（如 Traceview），记录 WPP 消息而不使用 IFR。

    ![在 visual studio 中启用 wpp 记录器](images/wpp-enable3.png)

5.  将驱动程序项目与 WppRecorder 链接。

    1.  在项目属性中，单击 "**配置属性**"，然后单击 "**链接器**"。
    2.  在 "**输入**" 下，将 " **$ （DDK\_库\_路径\\）** " 添加到 "**其他依赖项**" 字段。

    ![在 visual studio 中启用 wpp 记录器](images/wpp-enable4.png)

6.  将**Wpprecorder**添加到调用 IFR api 的每个源文件，例如[**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)设置你自己的 IFR 日志。 在[WPP\_INIT\_](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))在 KMDF 或 UMDF 2.15 驱动程序的*DriverEntry*例程中初始化跟踪调用之后调用 api。

## <a name="span-iduse__the_default_logspanspan-iduse__the_default_logspanspan-iduse__the_default_logspanuse-the-default-log"></a><span id="Use__the_default_log"></span><span id="use__the_default_log"></span><span id="USE__THE_DEFAULT_LOG"></span>使用默认日志


为驱动程序项目启用 WPP 后，WPP 会创建默认日志。 WPP 打印的默认日志的缓冲区大小为4096字节。 对于调试版本，缓冲区为24576字节。

如果默认日志缓冲区未能分配，则跟踪消息将发送到 WPP。 也就是说，不会通过 IFR 记录跟踪消息，但仍会将跟踪视为实时 WPP 跟踪。 若要确定是否已创建默认日志，驱动程序必须调用[**WppRecorderIsDefaultLogAvailable**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn914614(v=vs.85))。 如果默认日志不存在并且驱动程序要使用 IFR，则驱动程序必须创建日志。 有关详细信息，请参阅[创建自定义日志](#create)。

1.  初始化记录器\_通过调用[**记录器\_配置\_参数\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-recorder_configure_params_init)来[**配置\_的 params**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_configure_params)结构。 宏将**CreateDefaultLog**成员设置为 TRUE，这表示驱动程序要使用默认日志。
2.  通过指定[ **\_配置\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_configure_params)结构的已初始化记录器的地址来调用[**WppRecorderConfigure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderconfigure) 。
3.  可以通过调用[**WppRecorderLogGetDefault**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn895240(v=vs.85))获取记录器\_日志中的不透明句柄。
4.  通过调用在 node.js 中声明的跟踪宏，将跟踪消息打印到默认日志。 有关详细信息，请参阅[定义跟踪函数](#define)。
5.  在调试器中查看跟踪消息。 有关详细信息，请参阅[查看跟踪消息](#view)。

**注意** 若要禁用默认日志，请设置记录器的**CreateDefaultLog**成员[ **\_将\_参数配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_configure_params)为 FALSE，然后调用[**WppRecorderConfigure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderconfigure)。



在此示例中，驱动程序将获取默认日志的句柄。

```ManagedCPlusPlus

NTSTATUS
DriverEntry(
_In_ PDRIVER_OBJECT  DriverObject,
_In_ PUNICODE_STRING RegistryPath
)
{
    WDF_DRIVER_CONFIG config;
    NTSTATUS status;
    WDF_OBJECT_ATTRIBUTES attributes;

    RECORDER_CONFIGURE_PARAMS recorderConfig;

    RECORDER_LOG logHandle = NULL;

        // Initialize WPP Tracing.

    WPP_INIT_TRACING(DriverObject, RegistryPath);

    // If a default log is available, store the handle to the default log.

    if (WppRecorderIsDefaultLogAvailable())
    {
        RECORDER_CONFIGURE_PARAMS_INIT(&recorderConfig);

        WppRecorderConfigure(&recorderConfig);

        logHandle = WppRecorderLogGetDefault();

    }

    PrintEvents(logHandle, TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    //
    // Register a cleanup callback so that we can call WPP_CLEANUP when
    // the framework driver object is deleted during driver unload.
    //
    WDF_OBJECT_ATTRIBUTES_INIT(&attributes);
    attributes.EvtCleanupCallback = KMDFWPPEvtDriverContextCleanup;

    WDF_DRIVER_CONFIG_INIT(&config,
        KMDFWPPEvtDeviceAdd
        );

    status = WdfDriverCreate(DriverObject,
        RegistryPath,
        &attributes,
        &config,
        WDF_NO_HANDLE
        );

    if (!NT_SUCCESS(status)) {
        PrintEvents(logHandle, TRACE_LEVEL_ERROR, TRACE_DRIVER, "WdfDriverCreate failed %!STATUS!", status);
        WPP_CLEANUP(DriverObject);
        return status;
    }

    PrintEvents(logHandle, TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Exit");

    return status;
}
```

## <a name="span-idcreatespanspan-idcreatespancreate-a-custom-log-kernel-mode-drivers-only"></a><span id="create"></span><span id="CREATE"></span>创建自定义日志（仅限内核模式驱动程序）


IFR 的默认日志使用非分页池内存块4096。 所有跟踪消息都将写入循环缓冲区。 有时，最新消息可以覆盖以前的消息。

例如，你的驱动程序为控制和数据传输请求提供了不同的流路径。 如果两个活动中的活动都记录到同一个缓冲区，则数据传输消息将覆盖控件跟踪消息。 在这种情况下，可以为这些请求配置单独的缓冲区。

在另一个示例中，你有两个设备，一个设备比另一个设备发送更多跟踪消息。 如果驱动程序使用默认日志，该设备可能会淹没缓冲区，并且可能会删除来自其他设备的消息。 相反，驱动程序可以创建两个自定义日志，以便每个设备可以将消息发送到其缓冲区，并且可以单独查看每个设备的消息。

1.  初始化[**记录器\_日志\_创建\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_log_create_params)结构，方法是：调用[**记录器\_日志\_\_INIT 创建\_params**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-recorder_log_create_params_init)。 WPP 使用默认的日志参数，除非修改了结构的成员。
2.  可选。 将**TotalBufferSize**成员设置为所需的大小。 默认情况下，该大小设置为1024字节（请参阅录像机\_日志\_默认\_缓冲区\_大小（Wpprecorder）。
    **注意** WPP 从非分页池为日志分配缓冲区。 日志分为两个称为 "分区：常规" 和 "错误" 的循环缓冲区。 错误分区只显示跟踪\_级别\_错误的消息。 与所有其他级别相关的消息将发送到 "常规" 分区。 分区旨在防止详细的跟踪提供程序用较低优先级的消息覆盖其自己的错误消息。 调用方在**TotalBufferSize**中指定缓冲区大小，以指示这些分区的总大小。 错误分区不能超过总缓冲区大小的一半。 可以在初始化之后修改缓冲区大小。



3.  可选。 将**LogIdentifier**设置为一个字符串，该字符串将帮助你识别此缓冲区中的跟踪消息。 字符串长度不能超过16个字符。
4.  通过指定[ **\_日志\_创建\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_log_create_params)结构的已填充记录器的地址来调用[**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate) 。
5.  通过调用跟踪宏并通过[**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)调用接收的记录器\_日志句柄，将跟踪消息打印到此新缓冲区。
6.  在调试器中查看跟踪消息。 有关详细信息，请参阅[查看跟踪消息](#view)。

系统在注册表中定义最大和最小缓冲区大小。 可以适当地设置这些值，以节省内存和配置日志记录功能。

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\<serviceName>\Parameters
   WppRecorder_PerBufferMinBytes
   Data type
   REG_DWORD
   Description
   The minimum number of bytes that can be allocated to a  log buffer.  The default is 256 bytes.

   WppRecorder_PerBufferMaxBytes
   Data type
   REG_DWORD
   Description
   The maximum number of bytes that can be allocated to a  log buffer.  The default is 8192 bytes.

   LogPages
   Data type
   REG_DWORD
   Description
   The number of pages to store the default log. The default is 1.

   VerboseOn
   Data type
   REG_DWORD
   Description
   By default (0), IFR only logs errors, warnings, and informational events. Setting this value to 1 adds the verbose output to get logged. 
```

如果在记录器中指定的大小[ **\_LOG\_CREATE\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_log_create_params)小于最小字节数，则[**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)将分配**WppRecorder\_PerBufferMinBytes**字节。 同样，如果大小超过最大值，则**WppRecorderLogCreate**将分配**WppRecorder\_PerBufferMaxBytes**字节。

若要删除自定义日志，请在调用 WppRecorderLogDelete 之前调用[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogdelete) ， [\_清理](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))。 线程进入此函数后，所有线程都不能再登录到此缓冲区。 可以在驱动程序的[*EvtDriverUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)实现中调用此函数。

此代码示例是驱动程序的 DriverEntry 函数的代码片段。 在此示例中，驱动程序禁用默认日志，创建自定义日志，并设置其缓冲区大小和标识符。

```ManagedCPlusPlus
ULONG MyDriverLogSize = 8 * 1024;

NTSTATUS
DriverEntry(
_In_ PDRIVER_OBJECT  DriverObject,
_In_ PUNICODE_STRING RegistryPath
)
{
    WDF_DRIVER_CONFIG config;
    NTSTATUS status;
    WDF_OBJECT_ATTRIBUTES attributes;

    RECORDER_CONFIGURE_PARAMS recorderConfig;

    RECORDER_LOG_CREATE_PARAMS recorderCreate;

    RECORDER_LOG logHandle = NULL;

    // Initialize WPP Tracing.

    WPP_INIT_TRACING(DriverObject, RegistryPath);
    // If a default log is available, then configure the size of the buffer.
    // Store the handle to the default log and use it to set the identifier name.

    RECORDER_CONFIGURE_PARAMS_INIT(&recorderConfig);

    recorderConfig.CreateDefaultLog = FALSE;

    RECORDER_LOG_CREATE_PARAMS_INIT(&recorderCreate, NULL);
    recorderCreate.TotalBufferSize = MyDriverLogSize;
    RtlStringCbPrintfA(recorderCreate.LogIdentifier,
        RECORDER_LOG_IDENTIFIER_MAX_CHARS,
        "KMDFWpp_Log");

    status = WppRecorderLogCreate(&recorderCreate, &logHandle);
    if (!NT_SUCCESS(status))
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DRIVER, "WppRecorderLogCreate failed %!STATUS!", status);
    }

    PrintEvents(logHandle, TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    //
    // Register a cleanup callback so that we can call WPP_CLEANUP when
    // the framework driver object is deleted during driver unload.
    //
    WDF_OBJECT_ATTRIBUTES_INIT(&attributes);
    attributes.EvtCleanupCallback = KMDFWPPEvtDriverContextCleanup;

    WDF_DRIVER_CONFIG_INIT(&config,
        KMDFWPPEvtDeviceAdd
        );

    status = WdfDriverCreate(DriverObject,
        RegistryPath,
        &attributes,
        &config,
        WDF_NO_HANDLE
        );

    if (!NT_SUCCESS(status)) {
        PrintEvents(logHandle, TRACE_LEVEL_ERROR, TRACE_DRIVER, "WdfDriverCreate failed %!STATUS!", status);
        WPP_CLEANUP(DriverObject);
        return status;
    }

    PrintEvents(logHandle, TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Exit");

    return status;
}
```

## <a name="span-iddefinespanspan-iddefinespandefine-trace-functions"></a><span id="define"></span><span id="DEFINE"></span>定义跟踪函数


添加一个具有 "IFRLOG" 作为输入参数的跟踪函数（在你的 Trace .h 中）。 有关跟踪宏的信息，请参阅向[Windows 驱动程序添加 WPP 软件跟踪](adding-wpp-software-tracing-to-a-windows-driver.md)。

```ManagedCPlusPlus
//
// This comment block is scanned by the trace preprocessor to define our
// Trace function.
//
// begin_wpp config
// FUNC TraceEvents(LEVEL, FLAGS, MSG, ...);
// FUNC PrintEvents(IFRLOG, LEVEL, FLAGS, MSG, ...);
// end_wpp
//
```

在前面的示例中，有两个跟踪函数： TraceEvents 和 PrintEvents。 WPP 为具有在 FUNC 声明中指定的参数的函数生成宏。 在本主题中使用的示例中，驱动程序同时使用 TraceEvents 和 PrintEvents。 PrintEvents 要求 "IFRLOG" 作为参数。 调用此函数时，驱动程序必须将录像机\_日志句柄指定为 "IFRLOG" 的参数值。 仅当创建自定义缓冲区时，才会添加 IFRLOG。 TraceEvents 打印到默认日志。 这可以向后兼容现有的跟踪语句，而无需任何功能更改。

若要将跟踪消息打印到默认日志，驱动程序可以使用[**WppRecorderLogGetDefault**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn895240(v=vs.85))调用接收的句柄调用 PrintEvents，或者在没有句柄的情况下调用 TraceEvents。

若要打印到自定义日志，驱动程序会将对[**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)的调用中接收的句柄传递给。

## <a name="span-idmake__trace_messages_available_in_public_symbolsspanspan-idmake__trace_messages_available_in_public_symbolsspanspan-idmake__trace_messages_available_in_public_symbolsspanmake-trace-messages-available-in-public-symbols"></a><span id="Make__trace_messages_available_in_public_symbols"></span><span id="make__trace_messages_available_in_public_symbols"></span><span id="MAKE__TRACE_MESSAGES_AVAILABLE_IN_PUBLIC_SYMBOLS"></span>使跟踪消息可用于公共符号


在 WPP 中，需要[跟踪消息格式](trace-message-format-file.md)信息才能查看实际的 WPP 消息。 该信息存储在专用符号文件（Pdb）中。 TMF 信息自动包含在私有 PDB 中，而不是公共 PDB 中。 因此，不能查看没有专用 PDB 的消息。 若要将跟踪消息添加到公共 PDB，

若要使其中一些 WPP 跟踪消息成为公共的，必须向每条消息添加特殊标记。 在 Trace .h 文件中的定义之后添加 `// WPP_FLAGS(-public:<trace function name>)`。 标记在 WPP 命令行中由 **–公共**交换机指示。 该开关将添加到 WPP 预处理器，使其能够在公共 PDB 文件中保留 &lt;funcName&gt; 跟踪注释。

```ManagedCPlusPlus
//
// This comment block is scanned by the trace preprocessor to define our
// Trace function.
//
// begin_wpp config
// FUNC Trace{FLAG=MYDRIVER_ALL_INFO}(LEVEL, MSG, ...);
// FUNC TraceEvents(LEVEL, FLAGS, MSG, ...);
// FUNC PrintEvents(IFRLOG, LEVEL, FLAGS, MSG, ...);
// WPP_FLAGS(-public:PrintEvents);
// end_wpp
//
```

## <a name="span-idviewspanspan-idviewspanview-the-trace-messages"></a><span id="view"></span><span id="VIEW"></span>查看跟踪消息


若要查看跟踪消息，请使用 Windows 调试器中的[Wdfkd 扩展](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)。 扩展名为 Wdfkd。

1.  加载 Wdfkd 命令，在调试器中输入 `.load Wdfkd.dll`。
2.  使用这些命令可以查看跟踪消息。

    [ **!wdfkd.wdflogdump**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump)

    [ **!wdfkd.wdfcrashdump**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcrashdump)

内核模式驱动程序可以使用[RCDRKD 扩展](https://docs.microsoft.com/windows-hardware/drivers/debugger/rcdrkd-extensions)来查看跟踪日志。 用户模式驱动程序无法使用这些命令。

## <a name="span-idbest_practicesspanspan-idbest_practicesspanspan-idbest_practicesspanbest-practices"></a><span id="Best_practices"></span><span id="best_practices"></span><span id="BEST_PRACTICES"></span>最佳做法


-   在[WPP\_INIT\_](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))在内核模式驱动程序的*DriverEntry*例程中或在 UMDF 2.15 驱动程序的*DLLMain*例程中调用 IFR api。 如果全局策略禁用了日志记录，则调用 WPP\_INIT\_跟踪不会启用日志记录。

-   如果[**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)失败，则调用将返回 NULL 句柄。 在这种情况下，可以选择忽略**WppRecorderLogCreate**的返回值，并使用 RECODER\_日志句柄来打印 WPP 消息。

-   请勿删除[**WppRecorderLogGetDefault**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn895240(v=vs.85))返回的句柄。 若要禁用默认日志，请设置记录器的**CreateDefaultLog**成员[ **\_将\_参数配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/ns-wpprecorder-_recorder_configure_params)为 FALSE，然后调用[**WppRecorderConfigure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderconfigure)。

-   不要通过传递默认日志句柄来调用[**WppRecorderLogSetIdentifier**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogsetidentifier) 。 不允许执行该操作。

-   IFR 缓冲区是从非页面池分配的。 这些分配的累积总计效果可能导致明显的性能问题，尤其是在较小的占用空间的设备上。 请求[**WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)中较小的缓冲区大小。 而且，如果不需要日志记录功能，请禁用默认日志。

-   若要查看日志缓冲区的大小，请使用[ **！ wdfkd. wdflogdump**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump)命令。 如果使用的是[RCDRKD 扩展](https://docs.microsoft.com/windows-hardware/drivers/debugger/rcdrkd-extensions)，则可以使用[ **！ RCDRKD 查看大小。 rcdrloglist**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-rcdrkd-rcdrloglist)

## <a name="span-idumdf_and_kmdf_differencesspanspan-idumdf_and_kmdf_differencesspanspan-idumdf_and_kmdf_differencesspanumdf-and-kmdf-differences"></a><span id="UMDF_and_KMDF_differences"></span><span id="umdf_and_kmdf_differences"></span><span id="UMDF_AND_KMDF_DIFFERENCES"></span>UMDF 和 KMDF 差异


-   只有内核模式驱动程序可以创建自定义缓冲区。 此功能不适用于用户模式驱动程序。
-   不能使用[RCDRKD 扩展](https://docs.microsoft.com/windows-hardware/drivers/debugger/rcdrkd-extensions)从用户模式驱动程序中查看跟踪日志。 必须使用[Wdfkd 扩展](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)。









