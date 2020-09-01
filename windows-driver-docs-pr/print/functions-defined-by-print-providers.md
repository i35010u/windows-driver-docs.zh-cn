---
title: 打印提供程序定义的函数
description: 打印提供程序定义的函数
ms.assetid: 4fae4b69-ed4b-47b6-b6e8-41733aed51a5
keywords:
- 打印提供程序 WDK，函数
- 函数 WDK 打印提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38f2d2eb957dfddf56099f0564176b943a2c7887
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217189"
---
# <a name="functions-defined-by-print-providers"></a>打印提供程序定义的函数





**警告**   从 Windows 10 开始，不推荐使用支持第三方打印提供程序的 Api。 Microsoft 不建议对第三方打印提供商进行任何投资。 此外，在可用 v4 打印驱动程序模型的 Windows 8 和更高版本产品上，第三方打印提供商可能不会创建或管理使用 v4 打印驱动程序的队列。

 

本主题列出了打印提供商可提供的所有功能。 其中的大多数函数都在 Microsoft Windows SDK 文档中进行了介绍。 如果在 Windows 驱动程序工具包 (WDK) 中介绍了此函数，则函数名称将提供指向关联引用页的链接。

所有打印提供程序都必须为列出的所有函数提供指针。 但是，大多数供应商提供的打印提供程序都是 "部分提供程序"，它们不需要支持这些函数定义的许多操作。 因此，许多函数指针可以为 **NULL**。 有关部分打印提供程序的详细信息，请参阅 [编写网络打印提供程序](writing-a-network-print-provider.md)。

在以下函数列表中，必须支持的函数标记为 "Required"。

所有打印提供程序必须导出初始化函数 [**InitializePrintProvidor**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintprovidor)。 指向所有其他函数的指针必须在 [**PRINTPROVIDOR**](/windows-hardware/drivers/ddi/winsplp/ns-winsplp-_printprovidor) 结构中提供。  (请注意，这两个名称拼写错误，但与头文件 Winsplp 中显示的名称一致。 ) 

函数分为多个组，并在以下部分中提供：

初始化函数

打印队列管理功能

打印机驱动程序管理功能

打印作业创建函数

打印作业计划函数

窗体管理函数

打印处理器管理功能

打印监视器管理功能

端口管理函数

注册表管理功能

其他函数

### <a name="initialization-function"></a><a href="" id="ddk-initialization-function-gg"></a>初始化函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintprovidor" data-raw-source="[&lt;strong&gt;InitializePrintProvidor&lt;/strong&gt;](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintprovidor)"><strong>InitializePrintProvidor</strong></a> (必需) </p></td>
<td><p>初始化打印提供程序，并将指针返回到提供的函数。</p></td>
</tr>
</tbody>
</table>

 

### <a name="print-queue-management-functions"></a><a href="" id="ddk-print-queue-management-functions-gg"></a>打印队列管理功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Interactivesession.addprinter</strong></p></td>
<td><p>将打印队列添加到打印提供程序管理的列表中，并将打印处理器与打印队列相关联。</p></td>
</tr>
<tr class="even">
<td><p><strong>AddPrinterConnection</strong></p></td>
<td><p>创建与指定打印队列的连接。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClosePrinter</strong> (必需) </p></td>
<td><p>禁止调用方访问指定的打印队列。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeletePrinter</strong></p></td>
<td><p>从打印提供程序管理的列表中删除打印队列。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeletePrinterConnection</strong></p></td>
<td><p>删除与指定打印队列的连接。</p></td>
</tr>
<tr class="even">
<td><p><strong>EnumPrinters</strong> (必需) </p></td>
<td><p>枚举打印提供程序当前管理的打印队列的列表。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FindClosePrinterChangeNotification</strong></p></td>
<td><p>禁用由 <strong>FindFirstPrinterChangeNotification</strong>启用的打印机更改通知。</p></td>
</tr>
<tr class="even">
<td><p><strong>FindFirstPrinterChangeNotification</strong></p></td>
<td><p>返回等待对象的句柄，调用方可以使用该句柄等待指定的打印机事件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetPrinter</strong> (必需) </p></td>
<td><p>返回指定打印队列的当前参数值。</p></td>
</tr>
<tr class="even">
<td><p><strong>OpenPrinter</strong> (必需) </p></td>
<td><p>允许调用方访问指定的打印队列。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff561930(v=vs.85)" data-raw-source="[&lt;strong&gt;RefreshPrinterChangeNotification&lt;/strong&gt;](/previous-versions/ff561930(v=vs.85))"><strong>RefreshPrinterChangeNotification</strong></a></p></td>
<td><p>如果客户端调用 <strong>FindNextPrinterChangeNotification</strong> ，则由路由器调用 (参阅 Microsoft Windows SDK 文档) ，并设置 PRINTER_NOTIFY_OPTIONS_REFRESH 标志。</p></td>
</tr>
<tr class="even">
<td><p><strong>ResetPrinter</strong></p></td>
<td><p>修改打印队列的数据类型或 <a href="https://docs.microsoft.com/windows/win32/api/wingdi/ns-wingdi-devmodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](/windows/win32/api/wingdi/ns-wingdi-devmodew)"><strong>DEVMODEW</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SetPrinter</strong> (必需) </p></td>
<td><p>为指定的打印队列设置参数。</p></td>
</tr>
<tr class="even">
<td><p><strong>WaitForPrinterChange</strong></p></td>
<td><p>已过时。</p></td>
</tr>
</tbody>
</table>

 

### <a name="printer-driver-management-functions"></a><a href="" id="ddk-printer-driver-management-functions-gg"></a>打印机驱动程序管理功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddPrinterDriver</strong></p></td>
<td><p>将指定打印机的驱动程序文件添加到指定的服务器。</p></td>
</tr>
<tr class="even">
<td><p><strong>AddPrinterDriverEx</strong></p></td>
<td><p>与 <strong>AddPrinterDriver</strong>相同，具有附加参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeletePrinterDriver</strong></p></td>
<td><p>删除指定服务器上对指定打印机驱动程序文件的访问权限。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeletePrinterDriverEx</strong></p></td>
<td><p>与 <strong>DeletePrinterDriver</strong>相同，具有附加参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumPrinterDrivers</strong></p></td>
<td><p>返回已通过调用 <strong>AddPrinterDriver</strong> 或 <strong>AddPrinterDriverEx</strong>添加到指定服务器的打印机驱动程序列表。</p></td>
</tr>
<tr class="even">
<td><p><strong>GetPrinterDriver</strong></p></td>
<td><p>返回有关打印机驱动程序的信息，调用方可以将此信息传递给 <strong>AddPrinterDriver</strong>。  (通常从 INF 文件获取返回的信息。 ) </p></td>
</tr>
<tr class="odd">
<td><p><strong>GetPrinterDriverEx</strong></p></td>
<td><p>与 <strong>GetPrinterDriver</strong>相同，具有附加参数。</p></td>
</tr>
<tr class="even">
<td><p><strong>GetPrinterDriverDirectory</strong></p></td>
<td><p>返回服务器的打印机驱动程序目录的名称。</p></td>
</tr>
</tbody>
</table>

 

### <a name="print-job-creation-functions"></a><a href="" id="ddk-print-job-creation-functions-gg"></a>打印作业创建函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<strong>AbortPrinter</strong> (必需) </td>
<td><p>尝试从指定的打印队列中删除当前作业。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>System.printing.printqueue.addjob</strong> (必需) </td>
<td><p>返回作业标识符和假脱机文件路径。 调用方使用 <a href="https://docs.microsoft.com/windows/win32/api/fileapi/nf-fileapi-createfilea" data-raw-source="[&lt;strong&gt;CreateFile&lt;/strong&gt;](/windows/win32/api/fileapi/nf-fileapi-createfilea)"><strong>CreateFile</strong></a> 和 <strong>WriteFile</strong> 将数据发送到假脱机文件。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>EndDocPrinter</strong> (必需) </td>
<td><p>执行作业完成操作。</p></td>
</tr>
<tr class="even">
<td><p><strong>EndPagePrinter</strong></p></td>
<td><p>执行页面完成操作。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ReadPrinter</strong></p></td>
<td><p>从双向打印机获取状态信息。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>ScheduleJob</strong> (必需) </td>
<td><p>通知提供程序可以计划指定的作业。 作业由 <strong>system.printing.printqueue.addjob</strong>先前返回的作业标识符指定。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>StartDocPrinter</strong> (必需) </td>
<td><p>准备打印提供程序以开始对打印作业进行后台处理。</p></td>
</tr>
<tr class="even">
<td><p><strong>StartPagePrinter</strong></p></td>
<td><p>准备打印提供程序以接收打印作业页面。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>WritePrinter</strong> (必需) </td>
<td><p>接收打印作业的部分数据流。</p></td>
</tr>
</tbody>
</table>

 

**注意**   **System.printing.printqueue.addjob**.。。**ScheduleJob**序列是**StartDocPrinter**的一种替代方法。**EndDocPrinter**序列。

 

### <a name="print-job-scheduling-functions"></a><a href="" id="ddk-print-job-scheduling-functions-gg"></a>打印作业计划函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<strong>EnumJobs</strong> (必需) </td>
<td><p>返回计划的打印作业的列表。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>GetJob</strong> (必需) </td>
<td><p>返回作业参数。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>SetJob</strong> (必需) </td>
<td><p>取消、暂停、恢复或重新启动打印作业，或设置作业参数。</p></td>
</tr>
</tbody>
</table>

 

### <a name="forms-management-functions"></a><a href="" id="ddk-forms-management-functions-gg"></a>窗体管理函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddForm</strong></p></td>
<td><p>将指定的窗体添加到可用于指定打印机的列表。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeleteForm</strong></p></td>
<td><p>从可用于指定打印机的列表中删除指定的窗体。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumForms</strong></p></td>
<td><p>返回可用于指定打印机的窗体的列表。</p></td>
</tr>
<tr class="even">
<td><p><strong>GetForm</strong></p></td>
<td><p>返回指定窗体的特性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SetForm</strong></p></td>
<td><p>修改指定窗体的特征。</p></td>
</tr>
</tbody>
</table>

 

### <a name="print-processor-management-functions"></a><a href="" id="ddk-print-processor-management-functions-gg"></a>打印处理器管理功能

函数说明 **AddPrintProcessor**

将打印处理器安装在指定的服务器上，并将其添加到打印提供程序可调用的列的列表中。

**DeletePrintProcessor**

从打印提供程序可调用的打印处理器的列表中删除打印处理器。

**EnumPrintProcessorDataTypes**

返回打印提供程序可调用的打印处理器所支持的数据类型列表。

**EnumPrintProcessors**

返回打印提供程序可调用的打印处理器的列表。

**GetPrintProcessorDirectory**

返回必须存储打印处理器文件的目录路径。

 

### <a name="print-monitor-management-functions"></a><a href="" id="ddk-print-monitor-management-functions-gg"></a>打印监视器管理功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddMonitor</strong></p></td>
<td><p>将打印监视器添加到打印提供程序可调用的列表。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeleteMonitor</strong></p></td>
<td><p>从打印提供程序可调用的列的列表中删除打印监视器。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumMonitors</strong></p></td>
<td><p>返回打印提供程序可调用的打印监视器的列表。</p></td>
</tr>
</tbody>
</table>

 

### <a name="port-management-functions"></a><a href="" id="ddk-port-management-functions-gg"></a>端口管理函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddPort</strong></p></td>
<td><p>将打印机端口添加到可用的列表中，通常通过调用指定的端口监视器的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui" data-raw-source="[&lt;strong&gt;AddPortUI&lt;/strong&gt;](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui)"><strong>AddPortUI</strong></a> 函数。</p></td>
</tr>
<tr class="even">
<td><p><strong>AddPortEx</strong></p></td>
<td><p>与 <strong>AddPort</strong>相同，具有附加参数。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>ConfigurePort</strong> (必需) </td>
<td><p>配置打印机端口，通常通过调用指定的端口监视器的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui" data-raw-source="[&lt;strong&gt;ConfigurePortUI&lt;/strong&gt;](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui)"><strong>ConfigurePortUI</strong></a> 函数。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>DeletePort</strong> (必需) </td>
<td><p>从可用的列表中删除打印机端口，通常通过调用指定的端口监视器的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-deleteportui" data-raw-source="[&lt;strong&gt;DeletePortUI&lt;/strong&gt;](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-deleteportui)"><strong>DeletePortUI</strong></a> 函数。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>EnumPorts</strong> (必需) </td>
<td><p>返回可用打印机端口的列表。</p></td>
</tr>
<tr class="even">
<td><p><strong>SetPort</strong></p></td>
<td><p>设置指定打印机端口的参数。</p></td>
</tr>
</tbody>
</table>

 

### <a name="registry-management-functions"></a><a href="" id="ddk-registry-management-functions-gg"></a>注册表管理功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DeletePrinterData</strong></p></td>
<td><p>在指定打印机的 <strong>PrinterDriverData</strong> 键下删除当前分配给指定的值名称的值。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeletePrinterDataEx</strong></p></td>
<td><p>与 <strong>DeletePrinterData</strong>相同，具有附加参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeletePrinterKey</strong></p></td>
<td><p>如果指定的键及其子项当前存储在注册表中指定打印机的 <strong>PrinterDriverData</strong> 键下，则删除该项及其子项。</p></td>
</tr>
<tr class="even">
<td><p><strong>EnumPrinterData</strong></p></td>
<td><p>返回存储在注册表中指定打印机的 <strong>PrinterDriverData</strong> 键下的每个值名称和当前分配的值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumPrinterDataEx</strong></p></td>
<td><p>与 <strong>EnumPrinterData</strong>相同，具有附加参数。</p></td>
</tr>
<tr class="even">
<td><p><strong>EnumPrinterKey</strong></p></td>
<td><p>返回注册表中当前包含在指定的项名称下的子项列表。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetPrinterData</strong></p></td>
<td><p>返回当前分配给指定的值名称的值，该值存储在注册表中指定打印机的 <strong>PrinterDriverData</strong> 键下。</p></td>
</tr>
<tr class="even">
<td><p><strong>GetPrinterDataEx</strong></p></td>
<td><p>与 <strong>GetPrinterData</strong>相同，具有附加参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SetPrinterData</strong></p></td>
<td><p>在注册表中的指定打印机的 <strong>PrinterDriverData</strong> 项下存储指定的值名称和值。</p></td>
</tr>
<tr class="even">
<td><p><strong>SetPrinterDataEx</strong></p></td>
<td><p>与 <strong>SetPrinterData</strong>相同，具有附加参数。</p></td>
</tr>
</tbody>
</table>

 

### <a name="other-functions"></a><a href="" id="ddk-other-functions-gg"></a>其他函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff564255(v=vs.85)" data-raw-source="[&lt;strong&gt;XcvData&lt;/strong&gt;](/previous-versions/ff564255(v=vs.85))"><strong>XcvData</strong></a></p></td>
<td><p>提供端口监视器 UI DLL 和端口监视器服务器 DLL 之间的通信路径。</p></td>
</tr>
</tbody>
</table>

 

 

