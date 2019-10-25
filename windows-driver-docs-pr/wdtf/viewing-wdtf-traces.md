---
title: 启用和查看 WDTF 跟踪
description: 启用和查看 WDTF 跟踪
ms.assetid: 9bed6042-3691-4a5e-a143-51acf746b1ae
keywords:
- Windows 设备测试框架 WDK，跟踪事件
- WDTF WDK，跟踪事件
- 跟踪 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6665c1d431c660f5dfa152e013ca30e5a48fddbd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844798"
---
# <a name="enabling-and-viewing-wdtf-traces"></a>启用和查看 WDTF 跟踪

WDTF*跟踪*是指在 WDTF 对象内部发生的报告事件。 由于 WDTF 经过大量检测，因此所有 WDTF 对象都在运行时提供跟踪信息。 WDTF 使用[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)处理跟踪。 此类跟踪是一种标准化格式，可使用 WDK 工具（包括[TraceView](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-traceview)）进行读取。 本主题介绍了如何使用[Logman](https://go.microsoft.com/fwlink/p/?linkid=136332)和[Tracefmt](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracefmt)查看 WDTF 运行时跟踪。 本主题还讨论了如何以编程方式配置 WDTF 跟踪级别。

## <a name="how-to-collect-and-save-wdtf-traces"></a>如何收集和保存 WDTF 跟踪

### <a name="to-start-collecting-wdtf-traces"></a>开始收集 WDTF 跟踪

1. 在测试计算机上，使用提升的权限（以**管理员身份运行**）打开 "命令提示符" 窗口，然后输入以下命令：

    ```syntax
    logman.exe create trace "autosession\WDTF" -p {6210f559-c7f7-4d2f-b674-4bc9315cecc7} 0xffffffff 0xff -o c:\WDTF_Traces\TraceFile.etl
    reg add HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WDTF /v LogFileMode /t REG_DWORD /d 1 /f
    reg add HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WDTF /v FileMax /t REG_DWORD /d 16 /f
    reg add HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WDTF /v MaxFileSize /t REG_DWORD /d 0 /f
    ```

2. 重新启动计算机。

有关其他选项的信息，请参阅[Logman](https://go.microsoft.com/fwlink/p/?linkid=136332) （Logman）。 有关创建跟踪季节的信息，请参阅[配置和启动自动记录器会话](https://docs.microsoft.com/windows/desktop/ETW/configuring-and-starting-an-autologger-session)。

### <a name="to-stop-collecting-wdtf-traces-and-save-log-files"></a>停止收集 WDTF 跟踪并保存日志文件

1. 可以停止收集 WDTF 跟踪，并通过以下命令删除数据收集器：

    ```syntax
    logman.exe -stop -ets WDTF
    logman.exe delete "autosession\WDTF"
    ```

2. 重新启动计算机。
3. 将日志文件从测试计算机复制到另一台计算机，以供以后分析。

    收集的 ETL 日志文件大小可能非常大。 为获得最佳结果，请将测试计算机上的日志文件（例如，c：\\WDTF\_跟踪\\TraceFile）复制到另一台计算机。 然后，您可以从测试计算机中删除日志文件。

## <a name="how-to-view-wdtf-traces"></a>如何查看 WDTF 跟踪

查看 WDTF 跟踪要求设置 ETL 文件的格式。 以下步骤演示如何使用[Tracefmt](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracefmt)将 ETL 文件转换为文本文件或 CSV 文件。

### <a name="to-view-wdtf-traces"></a>查看 WDTF 跟踪

1. 例如，以下命令将已保存的 ETL 文件转换为 c：\\WDTF\_跟踪\\TraceFile 转换为文本。

    ```syntax
    Tracefmt.exe –r http://msdl.microsoft.com/download/symbols c:\WDTF_Traces\TraceFile.etl -o OutputTxtFile.txt
    ```

2. 以下命令将已保存为 c：\\WDTF\_跟踪的 ETL 文件转换为以逗号分隔的文件（CSV）\\TraceFile。

    ```syntax
    Tracefmt.exe –r http://msdl.microsoft.com/download/symbols c:\WDTF_Traces\TraceFile.etl -csv –o OutputCsvFile.csv
    ```

3. 在 Microsoft Excel 中打开 CSV 文件，以便您可以使用 Excel 的筛选功能来筛选收集的跟踪。 您可以在特定时间段内筛选跟踪。 可以筛选跟踪来检查某些 WDTF 组件记录的跟踪。

## <a name="programmatically-configuring-wdtf-trace-levels"></a>以编程方式配置 WDTF 跟踪级别

所有 WDTF 对象都在运行时提供跟踪信息。

WDTF 提供了一组可配置的[**TTraceLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)级别。 有关如何在运行时设置特定对象实例的**TTraceLevel**的信息，请参阅[**ITracing：： SetTraceLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)方法。

有关如何为接口设置默认[**TTraceLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)的信息，请参阅[Windows 设备测试框架参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

有关每个[**TTraceLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)中包含的跟踪类型的详细说明，请参阅[**ITracer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)接口。 你可以使用**ITracer**的注册表 TraceLevel 路径自行配置这些级别。

下表描述了可以设置的跟踪级别。

|级别|描述|
|----|----|
|0|“关”。 未提供任何跟踪。|
|1|低|
|2|Medium. 此级别为默认跟踪级别。|
|3|“高”|
|4|达到. 报告所有跟踪信息。|
|5-8|自定义级别。|
|9|将对象设置回其初始跟踪级别。|

当使用跟踪内容进行调试时，请考虑为所有对象将跟踪级别设置为1，然后为要检查的对象设置更高的跟踪级别。

有关跟踪级别的详细信息，请参阅[**ITracer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)接口。

## <a name="related-topics"></a>相关主题

[配置和启动自动记录器会话](https://docs.microsoft.com/windows/desktop/ETW/configuring-and-starting-an-autologger-session)  
[Logman](https://go.microsoft.com/fwlink/p/?linkid=136332)  
[Tracefmt](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracefmt)  
[TraceView](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-traceview)  
[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)  
