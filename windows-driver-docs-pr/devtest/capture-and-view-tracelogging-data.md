---
title: 捕获和查看 TraceLogging 数据
description: 捕获和查看 TraceLogging 数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f377d43d037e99cb8e99f743080208539a25aa88
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786383"
---
# <a name="capture-and-view-tracelogging-data"></a>捕获和查看 TraceLogging 数据


您可以使用 Windows 性能工具 (WPT) 的最新内部版本来捕获和查看 TraceLoggging 数据。 在发布检测之前，您应该测试您的 TraceLogging 提供程序代码，以确保生成事件数据并在适当的时间生成有意义的数据。

验证检测是否正确的过程包括以下两个步骤：

-   通过 Windows 性能记录器捕获跟踪 ( # A0 或 wprui.exe) 。
-   通过 Windows 性能分析器查看跟踪 ( # A0) 。

**注意**  对于 Windows Phone，还可以使用 Tracelog.exe 和 Xperf.exe 捕获跟踪。 请参阅下面的 "使用 Tracelog 和 XPerf 在手机 (上捕获跟踪") "。



### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件

"和 WPA 工具必须与要链接到的 TraceLogging 的版本兼容。 如果无法捕获或解码事件，可能是因为工具不匹配并且不兼容。

### <a name="span-idto_capture_trace_data_with_wprspanspan-idto_capture_trace_data_with_wprspanspan-idto_capture_trace_data_with_wprspanto-capture-trace-data-with-wpr"></a><span id="To_capture_trace_data_with_WPR"></span><span id="to_capture_trace_data_with_wpr"></span><span id="TO_CAPTURE_TRACE_DATA_WITH_WPR"></span>用 "捕获跟踪数据

1.  为 TraceLoggingProvider 创建或编辑 "配置文件 (. wprp) 。

    您可以使用以下示例。 将内容保存到文件扩展名为 wprp 的文件中。 将 TODO 节替换为提供程序的相应值。 例如，如果你按 GUID 注册了提供程序，请在此文件中指定 GUID。

    **注意**  对于内核模式提供程序，将 NonPagedMemory = "true" 添加到 EventProvider Id 元素，请参阅下面的 XML 示例中的注释。




示例 WPRP 文件：

```
<?xml version="1.0" encoding="utf-8"?>
<!-- TODO: 
1. Find and replace "WorkshopTraceLoggingProvider" with your component name.
2. See TODO below to update GUID for your event provider
-->
<WindowsPerformanceRecorder Version="1.0" Author="Microsoft Corporation" 
    Copyright="Microsoft Corporation" Company="Microsoft Corporation">
  <Profiles>
    <EventCollector Id="EventCollector_WorkshopTraceLoggingProvider" 
      Name="WorkshopTraceLoggingProviderCollector">
      <BufferSize Value="64" />
      <Buffers Value="4" />
    </EventCollector>

<!-- TODO: 
 1. Update Name attribute in EventProvider xml element with your provider GUID, 
    or if you specify an EventSource C# provider or call TraceLoggingRegister(...) 
    without a GUID, use star(*) before your provider name, 
    eg: Name="*MyEventSourceProvider" which will enable your provider appropriately.
 2. This sample lists more than 1 EventProvider xml element and references them again 
    in a Profile with EventProviderId xml element. For your component wprp, enable 
    the required number of providers and fix the Profile xml element appropriately
--> 
    <EventProvider Id="EventProvider_WorkshopTraceLoggingProvider" 
      Name="f9bc6c5d-4b98-43b5-90a1-1d0c8f45bf5a" />
<!-- For Kernel Mode providers, add NonPagedMemory="true" attribute to the 
  EventProvider Id element:

  Example:
  <EventProvider Id="EventProvider_UMDFReflector" 
    Name="263dd596-513b-4fd9-969c-022b691bb130" NonPagedMemory="true"/> 

-->

    <Profile Id="WorkshopTraceLoggingProvider.Verbose.File" 
      Name="WorkshopTraceLoggingProvider" Description="WorkshopTraceLoggingProvider" 
      LoggingMode="File" DetailLevel="Verbose">
      <Collectors>
        <EventCollectorId Value="EventCollector_WorkshopTraceLoggingProvider">
          <EventProviders>
<!-- TODO:
 1. Fix your EventProviderId with Value same as the Id attribute on EventProvider 
    xml element above
-->
            <EventProviderId Value="EventProvider_WorkshopTraceLoggingProvider" />
          </EventProviders>
        </EventCollectorId>
      </Collectors>
    </Profile>

    <Profile Id="WorkshopTraceLoggingProvider.Light.File" 
      Name="WorkshopTraceLoggingProvider" 
      Description="WorkshopTraceLoggingProvider" 
      Base="WorkshopTraceLoggingProvider.Verbose.File" 
      LoggingMode="File" 
      DetailLevel="Light" />

    <Profile Id="WorkshopTraceLoggingProvider.Verbose.Memory" 
      Name="WorkshopTraceLoggingProvider" 
      Description="WorkshopTraceLoggingProvider" 
      Base="WorkshopTraceLoggingProvider.Verbose.File" 
      LoggingMode="Memory" 
      DetailLevel="Verbose" />

    <Profile Id="WorkshopTraceLoggingProvider.Light.Memory" 
      Name="WorkshopTraceLoggingProvider" 
      Description="WorkshopTraceLoggingProvider" 
      Base="WorkshopTraceLoggingProvider.Verbose.File" 
      LoggingMode="Memory" 
      DetailLevel="Light" />

  </Profiles>
</WindowsPerformanceRecorder>
```


2.  对于内核模式提供程序，需要将 NonPagedMemory = "true" 属性添加到 EventProvider Id 元素中。

    ```
    <EventProvider Id="EventProvider_myTraceLoggingProviderKM" 
      Name="263dd596-513b-4fd9-969c-022b691bb130" NonPagedMemory="true"/>
    ```

3.  保存文件扩展名为 ( 的文件。WPRP) 。
4.  在命令提示符窗口中，使用 "启动捕获。

    ```
    <path to wpr>\wpr.exe -start GeneralProfile -start  yourTraceLoggingProvider.wprp
    ```

    GeneralProfile 将捕获系统事件。 对于常规调试，最好捕获系统事件以及提供程序中的事件。

5.  运行测试方案 (加载并卸载驱动程序或组件以触发事件) 。
6.  停止跟踪捕获并合并所有记录。

    ```
    <path to wpr>\wpr.exe -stop GeneralProfile -stop  yourTraceCaptureFile.etl description
    ```

你还可以使用 Windows 性能记录器用户界面 ( # A0) 收集跟踪数据。

```
<path to wpr>\wprui.exe
```

1.  如果隐藏了选项，请在 "" "窗口中单击" **更多选项**"。
2.  单击 " **添加配置文件** "，并浏览到你的 wprp 文件所在的位置。
3.  选择 wprp 文件并单击 " **打开**"。 "将验证您的配置文件的 XML 架构。
4.  单击 " **启动** " 并运行测试方案。
5.  单击 " **保存** " 以合并结果并将其保存到文件。 如果使用 "用户界面，则还会向你提供在 WPA 中打开 .etl 日志文件的选项。

### <a name="span-idto_capture_trace_on_phone__using_tracelog_and_xperf_spanspan-idto_capture_trace_on_phone__using_tracelog_and_xperf_spanspan-idto_capture_trace_on_phone__using_tracelog_and_xperf_spanto-capture-trace-on-phone-using-tracelog-and-xperf"></a><span id="To_capture_trace_on_Phone__using_Tracelog_and_XPerf_"></span><span id="to_capture_trace_on_phone__using_tracelog_and_xperf_"></span><span id="TO_CAPTURE_TRACE_ON_PHONE__USING_TRACELOG_AND_XPERF_"></span>使用 Tracelog 和 XPerf 在手机 (上捕获跟踪) 

1.  启动提供程序的跟踪捕获。

    ```
    cmdd tracelog '-start test -f c:\test.etl -guid #providerguid'
    ```

2.  运行测试方案以记录事件。
3.  停止跟踪捕获。

    ```
    cmdd tracelog '-stop test'
    ```

4.  合并跟踪结果。

    ```
    cmdd xperf -merge c:\test.etl c:\testmerged.etl
    ```

5.  检索合并的日志文件。

    ```
    getd c:\testmerged.etl
    ```

### <a name="span-idview_tracelogging_data_using_wpaspanspan-idview_tracelogging_data_using_wpaspanspan-idview_tracelogging_data_using_wpaspanview-tracelogging-data-using-wpa"></a><span id="View_TraceLogging_data_using_WPA"></span><span id="view_tracelogging_data_using_wpa"></span><span id="VIEW_TRACELOGGING_DATA_USING_WPA"></span>使用 WPA 查看 TraceLogging 数据

目前，WPA 是唯一可用于查看 TraceLogging 生成的 etl 文件的查看器。

1.  启动 WPA。

    ```
    <path to wpr>\wpa.exe
    ```

2.  将跟踪文件加载 ( .etl) 。
3.  查看提供程序事件。 在图形资源管理器中，展开 " **系统活动**"。
4.  双击 **一般事件** ，在分析视图中查看它们。
5.  在 "分析" 视图中，从提供程序中找到事件以验证日志记录是否正常工作。

    在 "通用事件" 表的 " **提供程序名称** " 列中，找到并选择包含提供程序名称的行。

    可以单击列标题以按列名排序，这样可以更轻松地找到提供者。 找到提供程序时，右键单击名称，然后选择 " **筛选器到选定内容**"。









