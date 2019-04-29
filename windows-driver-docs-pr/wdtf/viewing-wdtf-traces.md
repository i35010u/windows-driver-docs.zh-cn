---
title: 启用和查看 WDTF 跟踪
description: 启用和查看 WDTF 跟踪
ms.assetid: 9bed6042-3691-4a5e-a143-51acf746b1ae
keywords:
- Windows 设备测试框架 WDK，跟踪事件
- WDTF WDK、 跟踪事件
- 跟踪 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b346e581514c508ca7817b1796c62485c9f95e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323831"
---
# <a name="enabling-and-viewing-wdtf-traces"></a>启用和查看 WDTF 跟踪


WDTF*跟踪*指的是报告内 WDTF 对象内部发生的事件。 由于 WDTF 大量检测，所有 WDTF 对象将在运行时都提供跟踪信息。 WDTF 通过使用来处理跟踪[WPP 软件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556204)。 这种类型的跟踪是一种标准化的格式，可以通过使用 WDK 工具，包括读取[TraceView](https://msdn.microsoft.com/library/windows/hardware/ff556063)。 本主题介绍如何使用[Logman](https://go.microsoft.com/fwlink/p/?linkid=136332)并[Tracefmt](https://msdn.microsoft.com/library/windows/hardware/ff552974)视图 WDTF 运行时跟踪。 本主题还讨论了如何以编程方式配置 WDTF 跟踪级别。

-   [如何收集和保存 WDTF 跟踪](#how-to-collect)
-   [如何查看 WDTF 跟踪](#how-to-view)
-   [以编程方式配置 WDTF 跟踪级别](#wdtf-enable-level)

### <a href="" id="how-to-collect"></a>如何收集和保存 WDTF 跟踪

**若要开始收集 WDTF 跟踪**

1.  测试计算机上使用提升的权限打开命令提示符窗口 (**以管理员身份运行**)，并输入以下命令：

    ``` syntax
    logman.exe create trace "autosession\WDTF" -p {6210f559-c7f7-4d2f-b674-4bc9315cecc7} 0xffffffff 0xff -o c:\WDTF_Traces\TraceFile.etl
    reg add HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WDTF /v LogFileMode /t REG_DWORD /d 1 /f
    reg add HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WDTF /v FileMax /t REG_DWORD /d 16 /f
    reg add HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WDTF /v MaxFileSize /t REG_DWORD /d 0 /f
    ```

2.  重新启动计算机。

请参阅[Logman](https://go.microsoft.com/fwlink/p/?linkid=136332) (Logman.exe) 的其他选项的信息。 有关创建跟踪赛季的信息，请参阅[配置和启动自动记录器会话](https://msdn.microsoft.com/library/windows/desktop/aa363687)。

**若要停止收集 WDTF 跟踪并保存日志文件**

1.  你可以停止收集 WDTF 跟踪并删除数据收集器使用以下命令：

    ``` syntax
    logman.exe -stop -ets WDTF
    logman.exe delete "autosession\WDTF"
    ```

2.  重新启动计算机。
3.  从测试计算机的日志文件复制到另一台计算机以供日后分析。

    收集的 ETL 日志文件可能非常大的大小。 为获得最佳结果，从测试计算机复制的日志文件 (例如，c:\\WDTF\_跟踪\\TraceFile.etl) 到另一台计算机。 然后您可以从测试计算机中删除日志文件。

### <a href="" id="how-to-view"></a>如何查看 WDTF 跟踪

查看 WDTF 跟踪需要格式设置的 ETL 文件。 以下步骤演示如何使用[Tracefmt.exe](https://msdn.microsoft.com/library/windows/hardware/ff552974)将 ETL 文件转换为文本或 CSV 文件。

**若要查看 WDTF 跟踪**

1.  例如，以下命令将转换为 c： 已保存的 ETL 文件\\WDTF\_跟踪\\TraceFile.etl 为文本。

    ``` syntax
    Tracefmt.exe –r http://msdl.microsoft.com/download/symbols c:\WDTF_Traces\TraceFile.etl -o OutputTxtFile.txt
    ```

2.  以下命令将转换为 c： 已保存的 ETL 文件\\WDTF\_跟踪\\TraceFile.etl 到以逗号分隔 (CSV) 文件。

    ``` syntax
    Tracefmt.exe –r http://msdl.microsoft.com/download/symbols c:\WDTF_Traces\TraceFile.etl -csv –o OutputCsvFile.csv
    ```

3.  Microsoft Excel 中打开 CSV 文件，因此可以使用 Excel 的筛选功能筛选收集的跟踪。 您可以筛选跟踪某些时间段。 您可以筛选跟踪以检查记录的某些 WDTF 组件的跟踪。

## <a name="programmatically-configuring-wdtf-trace-levels"></a>以编程方式配置 WDTF 跟踪级别


在运行时，所有 WDTF 对象都提供跟踪信息。

WDTF 提供了一组可配置[ **TTraceLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff539616)级别。 有关如何设置的信息**TTraceLevel**的特定对象实例在运行时，请参阅[ **ITracing::SetTraceLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff539522)方法。

有关如何设置默认值的信息[ **TTraceLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff539616)对于接口，请参阅[Windows 设备测试框架引用](https://msdn.microsoft.com/library/windows/hardware/ff539647)。

有关详细的跟踪包含在每个类型的说明[ **TTraceLevel**](https://msdn.microsoft.com/library/windows/hardware/ff539616)，请参阅[ **ITracer** ](https://msdn.microsoft.com/library/windows/hardware/ff539512)接口。 可以全局这些级别自行配置使用**ITracer**的注册表 TraceLevel 路径。

下表介绍可以设置的跟踪级别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>级别</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>关闭。 不提供任何跟踪。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>低</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>媒体。 此级别是跟踪的默认级别。</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>高</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>完整。 报告所有跟踪信息。</p></td>
</tr>
<tr class="even">
<td><p>5-8</p></td>
<td><p>自定义级别。</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p>返回到其初始跟踪级别设置的对象。</p></td>
</tr>
</tbody>
</table>

 

通过使用跟踪内容调试时，请考虑将跟踪级别设置为 1 的所有对象，然后设置跟踪级别要检查的对象的要高得多。

有关跟踪级别的详细信息，请参阅[ **ITracer** ](https://msdn.microsoft.com/library/windows/hardware/ff539512)接口。

## <a name="related-topics"></a>相关主题
[配置和启动自动记录器会话](https://msdn.microsoft.com/library/windows/desktop/aa363687)  
[Logman](https://go.microsoft.com/fwlink/p/?linkid=136332)  
[Tracefmt](https://msdn.microsoft.com/library/windows/hardware/ff552974)  
[TraceView](https://msdn.microsoft.com/library/windows/hardware/ff556063)  
[WPP 软件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556204)  



