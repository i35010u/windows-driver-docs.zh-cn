---
title: 捕获和查看 TraceLogging 数据
description: 捕获和查看 TraceLogging 数据
ms.assetid: E5C18352-B05B-42BF-B5B8-12ABA0E6131C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b2ae5606fdff07fc29b8d8bd8ac0d1a80f60232
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375375"
---
# <a name="capture-and-view-tracelogging-data"></a>捕获和查看 TraceLogging 数据


您可以捕获并查看 TraceLoggging 数据使用内部的最新版本的 Windows 性能工具 (WPT)。 在发布之前的检测，应测试 TraceLogging 提供程序代码以确保您的活动数据将生成并在适当的时间生成有意义的数据。

验证程序的检测正确，涉及以下两个步骤：

-   与 Windows 性能记录器 （wpr.exe 或 wprui.exe） 捕获跟踪。
-   查看与 Windows 性能分析器 (wpa.exe) 的跟踪。

**请注意**为 Windows Phone 中，您还可用于 Tracelog.exe 和 Xperf.exe 捕获跟踪。 请参阅"在电话 （使用 Tracelog 和 XPerf） 上的跟踪进行捕获"下面。



### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件

WPR 和 WPA 工具必须与链接针对 TraceLogging 版本兼容。 如果无法捕获，或者对事件进行解码，则可能是因为工具不匹配和不兼容。

### <a name="span-idtocapturetracedatawithwprspanspan-idtocapturetracedatawithwprspanspan-idtocapturetracedatawithwprspanto-capture-trace-data-with-wpr"></a><span id="To_capture_trace_data_with_WPR"></span><span id="to_capture_trace_data_with_wpr"></span><span id="TO_CAPTURE_TRACE_DATA_WITH_WPR"></span>若要捕获与 WPR 跟踪数据

1.  创建或编辑你 TraceLoggingProvider WPR 配置文件 (.wprp)。

    可以使用下面的示例。 将内容保存到具有.wprp 文件扩展名的文件。 替换相应的值的 TODO 部分您的提供程序。 例如，如果您注册您的提供程序 guid，此文件中指定 GUID。

    **请注意**内核模式提供程序，将添加 NonPagedMemory ="true"EventProvider Id 元素，请参阅下面的 XML 示例中的注释。




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


2.  对于内核模式提供程序，您需要添加 NonPagedMemory ="true"属性设置为 EventProvider Id 元素。

    ```
    <EventProvider Id="EventProvider_myTraceLoggingProviderKM" 
      Name="263dd596-513b-4fd9-969c-022b691bb130" NonPagedMemory="true"/>
    ```

3.  使用文件扩展名保存文件 (。WPRP)。
4.  启动命令提示符窗口中使用 WPR 捕获。

    ```
    <path to wpr>\wpr.exe -start GeneralProfile -start  yourTraceLoggingProvider.wprp
    ```

    GeneralProfile 将捕获系统事件。 对于常规调试，它是捕获系统事件和发生的事件提供程序的一个好办法。

5.  运行测试方案 （加载和卸载驱动程序或触发事件的组件）。
6.  停止跟踪捕获和合并所有录制。

    ```
    <path to wpr>\wpr.exe -stop GeneralProfile -stop  yourTraceCaptureFile.etl description
    ```

Windows 性能记录器用户界面 (Wprui.exe) 还可用于收集跟踪数据。

```
<path to wpr>\wprui.exe
```

1.  在 WPR 窗口中，如果选项处于隐藏状态，请单击**更多选项**。
2.  单击**添加配置文件**并浏览到.wprp 文件的位置。
3.  选择.wprp 文件，然后单击**打开**。 WPR 将验证你的配置文件的 XML 架构。
4.  单击**启动**并运行测试方案。
5.  单击**保存**合并结果并将其保存到文件。 如果您使用 WPR 用户界面，您还可以选择在 WPA 中打开.etl 日志文件。

### <a name="span-idtocapturetraceonphoneusingtracelogandxperfspanspan-idtocapturetraceonphoneusingtracelogandxperfspanspan-idtocapturetraceonphoneusingtracelogandxperfspanto-capture-trace-on-phone-using-tracelog-and-xperf"></a><span id="To_capture_trace_on_Phone__using_Tracelog_and_XPerf_"></span><span id="to_capture_trace_on_phone__using_tracelog_and_xperf_"></span><span id="TO_CAPTURE_TRACE_ON_PHONE__USING_TRACELOG_AND_XPERF_"></span>若要跟踪 （使用 Tracelog 和 XPerf） 的 Phone 上捕获

1.  启动跟踪捕获的您的提供程序。

    ```
    cmdd tracelog '-start test -f c:\test.etl -guid #providerguid'
    ```

2.  运行你的测试方案来记录事件。
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

### <a name="span-idviewtraceloggingdatausingwpaspanspan-idviewtraceloggingdatausingwpaspanspan-idviewtraceloggingdatausingwpaspanview-tracelogging-data-using-wpa"></a><span id="View_TraceLogging_data_using_WPA"></span><span id="view_tracelogging_data_using_wpa"></span><span id="VIEW_TRACELOGGING_DATA_USING_WPA"></span>查看使用 WPA TraceLogging 数据

目前，WPA 是唯一的查看器可用于查看 TraceLogging 生成的 etl 文件。

1.  启动 WPA。

    ```
    <path to wpr>\wpa.exe
    ```

2.  加载跟踪文件 (.etl)。
3.  查看提供程序事件。 在图形资源管理器，展开**系统活动**。
4.  双击**泛型事件**分析视图中查看它们。
5.  在分析视图中，找到事件从提供程序验证日志记录正常工作。

    在中**提供程序名称**泛型事件表的列查找并选择包含您的提供程序名称的行。

    您可以单击列标题以按列名称，这可能会使更轻松地找到您的提供程序进行排序。 当发现提供程序，右键单击名称并选择**筛选器添加到所选内容**。









