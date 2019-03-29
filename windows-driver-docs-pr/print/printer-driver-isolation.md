---
title: 打印机驱动程序隔离
description: 打印机驱动程序隔离打印机驱动程序在独立于打印后台处理程序在其中运行的进程的进程中运行，从而提高了 Windows 打印服务的可靠性。
ms.assetid: b0f11b3f-92f7-41f6-8edb-63b5651f5499
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d60aeadbefa59113df234c245fb03116f98744c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569296"
---
# <a name="printer-driver-isolation"></a>打印机驱动程序隔离


打印机驱动程序隔离打印机驱动程序在独立于打印后台处理程序在其中运行的进程的进程中运行，从而提高了 Windows 打印服务的可靠性。

Windows 7、 Windows Server 2008 R2 和更高版本操作系统中实现的打印机驱动程序隔离的支持。

对于 Windows 7 和 Windows Server 2008 R2，收件箱打印机驱动程序必须支持打印机驱动程序隔离，并且能够在独立进程中运行。

### <a href="" id="previous-versions-of-windows"></a> 以前版本的 Windows

在以前版本的 Windows，包括 Windows Server 2008，打印机驱动程序始终运行为后台处理程序在同一进程中。 后台处理程序进程中运行的打印机驱动程序组件包括以下方面：

-   打印驱动程序配置模块

-   打印处理器

-   呈现模块

单个打印驱动程序组件的故障可能会导致打印子系统失败，正在停止打印操作为所有用户和适用于所有打印组件。

### <a href="" id="new-versions-of-windows"></a> 新版本的 Windows

借助 Windows 7 和 Windows Server 2008 R2，管理员可以作为一个选项，配置在独立的进程-是独立于后台处理程序进程的进程中运行的打印机驱动程序。 通过隔离该驱动程序，管理员可阻止驱动程序组件中的错误导致停止打印服务。

有关后台处理程序函数的详细信息，请参阅[后台处理程序组件函数和结构](https://msdn.microsoft.com/library/windows/hardware/ff562686)。

### <a href="" id="driver-isolation-support-in-inf-files"></a> INF 文件中的驱动程序隔离支持

默认情况下，如果安装的打印机驱动程序的 INF 文件并不表示该驱动程序支持驱动程序隔离打印机类安装程序将配置驱动程序在后台处理程序进程中运行。 但是，如果 INF 文件指示驱动程序支持驱动程序隔离，安装程序会配置在独立进程中运行的驱动程序。 管理员可以重写这些配置设置，并指定，对于每个驱动程序，是否在后台处理程序过程中或独立进程中运行驱动程序。

若要支持驱动程序隔离，安装打印机驱动程序的 INF 文件可以使用**驱动程序隔离**关键字来指示该驱动程序是否支持打印机驱动程序隔离。 设置**驱动程序隔离**= 2 指示驱动程序支持驱动程序隔离。 设置**驱动程序隔离**= 0 指示驱动程序不支持驱动程序隔离。 省略**驱动程序隔离**INF 文件中的关键字具有相同的效果与设置**驱动程序隔离**= 0。

### <a href="" id="spooler-functions-for-driver-isolation-settings"></a> 驱动程序隔离设置的后台处理程序函数

下表显示了管理员可以使用配置的驱动程序隔离设置的后台处理程序函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数名称</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=135631" data-raw-source="[GetPrinterDataEx](https://go.microsoft.com/fwlink/p/?linkid=135631)">GetPrinterDataEx</a></p></td>
<td><p>获取打印机的驱动程序隔离设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=135632" data-raw-source="[SetPrinterDataEx](https://go.microsoft.com/fwlink/p/?linkid=135632)">SetPrinterDataEx</a></p></td>
<td><p>设置打印机的驱动程序隔离设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=135633" data-raw-source="[EnumPrinterDataEx](https://go.microsoft.com/fwlink/p/?linkid=135633)">EnumPrinterDataEx</a></p></td>
<td><p>枚举的打印机驱动程序隔离设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=135634" data-raw-source="[FindFirstPrinterChangeNotification](https://go.microsoft.com/fwlink/p/?linkid=135634)">FindFirstPrinterChangeNotification</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=135635" data-raw-source="[FindNextPrinterChangeNotification](https://go.microsoft.com/fwlink/p/?linkid=135635)">FindNextPrinterChangeNotification</a></p></td>
<td><p>请求更改的通知给打印机的驱动程序隔离设置。</p></td>
</tr>
</tbody>
</table>

 

数据的格式如下所示：

-   每个组中的驱动程序分隔\\
-   通过分隔每个驱动程序组\\\\

第一个组将驱动程序加载到后台处理程序进程。 每个后续组加载每个组的隔离进程中的驱动程序。 第二个组会被视为默认加载其他支持隔离的驱动程序的共享组。

### <a href="" id="configuring-driver-isolation-mode-through-administration"></a> 通过管理的配置驱动程序隔离模式

计算机管理员可以使用 Windows 打印管理控制台或调用 Windows 后台处理程序函数来配置每个打印机驱动程序的计算机上安装的驱动程序隔离设置。 管理员配置驱动程序使用下表中列出的设置之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>驱动程序隔离模式</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>共享</p></td>
<td><p>与其他打印机驱动程序共享，但独立于后台处理程序进程的进程中运行驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>隔离</p></td>
<td><p>是独立于后台处理程序进程并不与其他打印机驱动程序共享的进程中运行驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p>无</p></td>
<td><p>在后台处理程序进程中运行该驱动程序。</p></td>
</tr>
</tbody>
</table>

 

理想情况下，打印机驱动程序就能够在共享模式下运行。 也就是说，它运行在一个独立的进程中共享与其他打印机驱动程序，但独立于后台处理程序进程。 驱动程序可能需要在独立模式下运行，当从后台处理程序过程中，可以在单独的进程中运行，但与其他驱动程序共享过程方面存在困难。 例如，设计欠佳的驱动程序可能具有与的相关驱动程序或不同版本的相同的驱动程序的操作相冲突的文件名称或驱动程序可能会经常发生故障或存在内存泄漏会干扰其他驱动程序中运行的操作在同一进程。

若要支持故障排除，域管理员可以禁用域中的计算机上的驱动程序隔离功能或管理员可强制所有打印机驱动程序在独立模式下运行的计算机上。 在独立模式下，必须单独从后台处理程序和其他打印机驱动程序的进程中运行每个驱动程序。

如果通过组策略禁用了驱动程序隔离，隔离是关闭的所有打印机驱动程序。 如果启用了隔离，单个驱动程序是模式检查。 如果驱动程序包含隔离模式设置，它将运行中共享，隔离，或无模式下，基于注册表项。 但是，如果驱动程序不具备隔离模式设置，并且它与隔离都兼容，它运行在共享模式下。 如果该驱动程序不兼容模式下，组策略替代确定驱动程序是否运行在共享的模式或无模式。

下图显示了选择驱动程序隔离模式的决策映射：

![选择驱动程序隔离模式的流程图](images/isolation.png)

### <a name="spooler-functions-allowed-under-driver-isolation"></a>允许在驱动程序隔离级别下的后台处理程序函数

在驱动程序隔离级别下允许仅特定的函数。

### <a href="" id="spoolss-dll-functions"></a>Spoolss.dll 函数

以下函数由 spoolss.dll 导出并可供后台处理程序插件通过链接到 spoolss.lib。

**AddMonitorW**

**AppendPrinterNotifyInfoData**

**ClosePrinter**

**DeletePortW**

**DeletePrintProcessorW**

**EndDocPrinter**

**EndPagePrinter**

**EnumFormsW**

**EnumJobsW**

**FlushPrinter**

**GetJobAttributes**

**GetJobAttributesEx**

**GetJobW**

**GetPrinterDataExW**

**GetPrinterDataW**

**GetPrinterDriverDirectoryW**

**GetPrinterDriverW**

**GetPrinterW**

**ImpersonatePrinterClient**

**OpenPrinterW**

**ReadPrinter**

**RouterCreatePrintAsyncNotificationChannel**

**RouterGetPrintClassObject**

**SetJobW**

**SetPrinterDataExW**

**SetPrinterDataW**

**StartDocPrinterW**

**StartPagePrinter**

**WritePrinter**

### <a href="" id="winspool-drv-functions"></a>WinSpool.drv 函数

以下函数由 winspool.drv 导出并可供后台处理程序插件通过链接到 Winspool.h。

**AppendPrinterNotifyInfoData**

**ExtDeviceMode**

**ImpersonatePrinterClient**

**IsValidDevmode**

**PartialReplyPrinterChangeNotification**

**ReplyPrinterChangeNotification**

**RevertToPrinterSelf**

**RouterAllocBidiMem**

**RouterAllocBidiResponseContainer**

**RouterAllocPrinterNotifyInfo**

**RouterCreatePrintAsyncNotificationChannel**

**RouterFreeBidiMem**

**RouterFreeBidiResponseContainer**

**RouterFreePrinterNotifyInfo**

**RouterGetPrintClassObject**

**RouterRegisterForPrintAsyncNotifications**

**RouterUnregisterForPrintAsyncNotifications**

 

 




