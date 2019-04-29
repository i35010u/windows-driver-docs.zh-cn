---
title: 打印提供程序定义的函数
description: 打印提供程序定义的函数
ms.assetid: 4fae4b69-ed4b-47b6-b6e8-41733aed51a5
keywords:
- 打印提供程序 WDK，函数
- 函数 WDK 打印提供商
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ec343fd5db0345044216287d0d559aa4c32d43f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363445"
---
# <a name="functions-defined-by-print-providers"></a>打印提供程序定义的函数





**警告**  从 Windows 10 开始，支持第三方打印提供商的 Api 已弃用。 Microsoft 不建议到第三方打印提供商的任何投资。 此外，在 Windows 8 和更高版本的 v4 打印驱动程序模型是可用的产品，第三方打印提供商不可能创建，或管理使用 v4 打印驱动程序的队列。

 

本主题列出了所有打印提供程序可以提供的函数。 Microsoft Windows SDK 文档中描述了其中的大多数功能。 如果该函数描述 Windows Driver Kit (WDK) 中，函数名称提供了指向关联的参考页的链接。

所有打印提供商必须提供所有列出的函数的指针。 但是，大多数供应商提供的打印提供商为"部分提供程序"这不需要支持的许多操作定义的函数。 因此，许多函数指针可以**NULL**。 有关部分打印提供程序的详细信息，请参阅[编写网络打印提供商](writing-a-network-print-provider.md)。

在下面的函数列表中，必须支持的函数被标为"Required"。

所有打印提供商必须导出初始化函数， [ **InitializePrintProvidor**](https://msdn.microsoft.com/library/windows/hardware/ff551614)。 所有其他函数的指针必须提供[ **PRINTPROVIDOR** ](https://msdn.microsoft.com/library/windows/hardware/ff560993)结构。 （请注意这两个名称都拼写错误，但与标头文件，Winsplp.h 中出现的名称保持一致）。

函数是划分为组，并且显示以下各节中：

初始化函数

打印队列管理功能

打印机驱动程序管理功能

打印作业创建函数

打印作业计划功能

窗体管理功能

打印处理器管理功能

打印监视器管理功能

端口的管理功能

注册表管理函数

其他函数

### <a href="" id="ddk-initialization-function-gg"></a>初始化函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551614" data-raw-source="[&lt;strong&gt;InitializePrintProvidor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551614)"><strong>InitializePrintProvidor</strong> </a> （必需）</p></td>
<td><p>初始化的打印提供程序，并返回到提供的函数的指针。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-print-queue-management-functions-gg"></a>打印队列管理功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddPrinter</strong></p></td>
<td><p>将打印队列添加到列表的管理的打印提供程序，并将打印处理器与打印队列相关联。</p></td>
</tr>
<tr class="even">
<td><p><strong>AddPrinterConnection</strong></p></td>
<td><p>创建与指定的打印队列的连接。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClosePrinter</strong> （必需）</p></td>
<td><p>禁用对指定的打印队列的调用方访问。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeletePrinter</strong></p></td>
<td><p>从管理的打印提供程序的列表中删除打印队列。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeletePrinterConnection</strong></p></td>
<td><p>移除与指定的打印队列的连接。</p></td>
</tr>
<tr class="even">
<td><p><strong>EnumPrinters</strong> （必需）</p></td>
<td><p>枚举当前管理的打印提供程序的打印队列的列表。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FindClosePrinterChangeNotification</strong></p></td>
<td><p>禁用打印机更改通知的情况下将启用<strong>FindFirstPrinterChangeNotification</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>FindFirstPrinterChangeNotification</strong></p></td>
<td><p>返回到调用方可以使用等待指定的打印机事件的等待对象的句柄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetPrinter</strong> （必需）</p></td>
<td><p>返回指定的打印队列的当前参数值。</p></td>
</tr>
<tr class="even">
<td><p><strong>OpenPrinter</strong> （必需）</p></td>
<td><p>实现对指定的打印队列的调用方访问。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561930" data-raw-source="[&lt;strong&gt;RefreshPrinterChangeNotification&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561930)"><strong>RefreshPrinterChangeNotification</strong></a></p></td>
<td><p>如果客户端调用名为路由器<strong>FindNextPrinterChangeNotification</strong> （请参阅 Microsoft Windows SDK 文档） 与 PRINTER_NOTIFY_OPTIONS_REFRESH 标志设置。</p></td>
</tr>
<tr class="even">
<td><p><strong>ResetPrinter</strong></p></td>
<td><p>修改打印队列的数据类型或<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SetPrinter</strong> （必需）</p></td>
<td><p>设置用于指定的打印队列的参数。</p></td>
</tr>
<tr class="even">
<td><p><strong>WaitForPrinterChange</strong></p></td>
<td><p>已过时。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-printer-driver-management-functions-gg"></a>打印机驱动程序管理功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddPrinterDriver</strong></p></td>
<td><p>将指定的打印机驱动程序文件添加到指定的服务器。</p></td>
</tr>
<tr class="even">
<td><p><strong>AddPrinterDriverEx</strong></p></td>
<td><p>与相同<strong>AddPrinterDriver</strong>，使用其他参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeletePrinterDriver</strong></p></td>
<td><p>对指定的打印机驱动程序文件，指定服务器上删除访问。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeletePrinterDriverEx</strong></p></td>
<td><p>与相同<strong>DeletePrinterDriver</strong>，使用其他参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumPrinterDrivers</strong></p></td>
<td><p>返回通过调用添加到指定的服务器的打印机驱动程序的列表<strong>AddPrinterDriver</strong>或<strong>AddPrinterDriverEx</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>GetPrinterDriver</strong></p></td>
<td><p>返回有关打印机驱动程序，然后可以将调用方传递到的信息<strong>AddPrinterDriver</strong>。 （返回的信息通常从获取 INF 文件。）</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetPrinterDriverEx</strong></p></td>
<td><p>与相同<strong>GetPrinterDriver</strong>，使用其他参数。</p></td>
</tr>
<tr class="even">
<td><p><strong>GetPrinterDriverDirectory</strong></p></td>
<td><p>返回的名称服务器的打印机驱动程序目录。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-print-job-creation-functions-gg"></a>打印作业创建函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<strong>AbortPrinter</strong> （必需）</td>
<td><p>尝试从指定的打印队列中删除当前的作业。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>AddJob</strong> （必需）</td>
<td><p>返回的作业标识符和假脱机文件路径。 调用方将使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa363858" data-raw-source="[&lt;strong&gt;CreateFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363858)"> <strong>CreateFile</strong> </a>并<strong>WriteFile</strong>将数据发送到后台打印文件。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>EndDocPrinter</strong> （必需）</td>
<td><p>执行作业完成操作。</p></td>
</tr>
<tr class="even">
<td><p><strong>EndPagePrinter</strong></p></td>
<td><p>执行页完成操作。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ReadPrinter</strong></p></td>
<td><p>从双向打印机获取状态信息。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>ScheduleJob</strong> （必需）</td>
<td><p>通知提供程序可以计划指定的作业。 作业由以前返回的作业标识符<strong>AddJob</strong>。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>StartDocPrinter</strong> （必需）</td>
<td><p>准备要开始在后台处理打印作业的打印提供程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>StartPagePrinter</strong></p></td>
<td><p>准备要接收打印作业页的打印提供程序。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>WritePrinter</strong> （必需）</td>
<td><p>接收打印作业的数据的流的一部分。</p></td>
</tr>
</tbody>
</table>

 

**请注意**   **AddJob**...**ScheduleJob**序列是一种替代方法**StartDocPrinter**...**EndDocPrinter**序列。

 

### <a href="" id="ddk-print-job-scheduling-functions-gg"></a>打印作业计划功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<strong>EnumJobs</strong> （必需）</td>
<td><p>返回计划的打印作业的列表。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>GetJob</strong> （必需）</td>
<td><p>返回作业参数。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>SetJob</strong> （必需）</td>
<td><p>取消、 暂停、 继续时，或重新启动打印作业，或设置作业参数。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-forms-management-functions-gg"></a>窗体管理功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddForm</strong></p></td>
<td><p>将指定的窗体添加到这些可用于指定打印机的列表。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeleteForm</strong></p></td>
<td><p>这些可用于指定打印机列表中移除指定的窗体。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumForms</strong></p></td>
<td><p>返回窗体可用于指定打印机的列表。</p></td>
</tr>
<tr class="even">
<td><p><strong>GetForm</strong></p></td>
<td><p>返回指定的窗体的特征。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SetForm</strong></p></td>
<td><p>修改指定的窗体的特征。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-print-processor-management-functions-gg"></a>打印处理器管理功能

函数说明**AddPrintProcessor**

指定的服务器上安装打印处理器，并将其添加到其中的打印提供程序可以调用列表。

**DeletePrintProcessor**

从这些打印提供程序可以调用列表中删除打印处理器。

**EnumPrintProcessorDataTypes**

返回由打印提供程序可调用的打印处理器支持的数据类型的列表。

**EnumPrintProcessors**

返回打印提供程序可以调用的打印处理器的列表。

**GetPrintProcessorDirectory**

返回的打印处理器文件必须存储在其中的目录路径。

 

### <a href="" id="ddk-print-monitor-management-functions-gg"></a>打印监视器管理功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddMonitor</strong></p></td>
<td><p>向这些打印提供程序可以调用列表中添加打印监视器。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeleteMonitor</strong></p></td>
<td><p>从这些打印提供程序可以调用列表中删除打印监视器。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumMonitors</strong></p></td>
<td><p>返回打印提供程序可以调用的打印监视器的列表。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-port-management-functions-gg"></a>端口的管理功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddPort</strong></p></td>
<td><p>将添加到列表的可用，打印机端口，通常通过调用指定的端口监视器<a href="https://msdn.microsoft.com/library/windows/hardware/ff545026" data-raw-source="[&lt;strong&gt;AddPortUI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545026)"> <strong>AddPortUI</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td><p><strong>AddPortEx</strong></p></td>
<td><p>与相同<strong>端口</strong>，使用其他参数。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>ConfigurePort</strong> （必需）</td>
<td><p>配置打印机端口，通常通过调用指定的端口监视器<a href="https://msdn.microsoft.com/library/windows/hardware/ff546290" data-raw-source="[&lt;strong&gt;ConfigurePortUI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546290)"> <strong>ConfigurePortUI</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>DeletePort</strong> （必需）</td>
<td><p>删除打印机端口从列表中的可用，通常通过调用指定的端口监视器<a href="https://msdn.microsoft.com/library/windows/hardware/ff547432" data-raw-source="[&lt;strong&gt;DeletePortUI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547432)"> <strong>DeletePortUI</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>EnumPorts</strong> （必需）</td>
<td><p>返回可用的打印机端口的列表。</p></td>
</tr>
<tr class="even">
<td><p><strong>SetPort</strong></p></td>
<td><p>设置用于指定的打印机端口的参数。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-registry-management-functions-gg"></a>注册表管理函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DeletePrinterData</strong></p></td>
<td><p>删除当前分配给指定的值名称，在指定的打印机下的值<strong>PrinterDriverData</strong>密钥。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeletePrinterDataEx</strong></p></td>
<td><p>与相同<strong>DeletePrinterData</strong>，使用其他参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeletePrinterKey</strong></p></td>
<td><p>删除指定的项及其子项，如果它们当前存储在注册表中指定的打印机下<strong>PrinterDriverData</strong>密钥。</p></td>
</tr>
<tr class="even">
<td><p><strong>EnumPrinterData</strong></p></td>
<td><p>返回每个值名称的目前分配值存储在注册表项下指定的打印机<strong>PrinterDriverData</strong>密钥。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumPrinterDataEx</strong></p></td>
<td><p>与相同<strong>EnumPrinterData</strong>，使用其他参数。</p></td>
</tr>
<tr class="even">
<td><p><strong>EnumPrinterKey</strong></p></td>
<td><p>返回当前包含在注册表中指定的密钥名称下的子项的列表。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetPrinterData</strong></p></td>
<td><p>返回当前分配给指定的值名称，它存储在注册表项下指定的打印机的值<strong>PrinterDriverData</strong>密钥。</p></td>
</tr>
<tr class="even">
<td><p><strong>GetPrinterDataEx</strong></p></td>
<td><p>与相同<strong>GetPrinterData</strong>，使用其他参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SetPrinterData</strong></p></td>
<td><p>将指定的值名称和值存储在注册表中，在指定的打印机<strong>PrinterDriverData</strong>密钥。</p></td>
</tr>
<tr class="even">
<td><p><strong>SetPrinterDataEx</strong></p></td>
<td><p>与相同<strong>SetPrinterData</strong>，使用其他参数。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-other-functions-gg"></a>其他函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564255" data-raw-source="[&lt;strong&gt;XcvData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564255)"><strong>XcvData</strong></a></p></td>
<td><p>提供端口监视器 UI DLL 和端口监视服务器 DLL 之间的通信路径。</p></td>
</tr>
</tbody>
</table>

 

 

 




