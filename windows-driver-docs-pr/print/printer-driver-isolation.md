---
title: 打印机驱动程序隔离
description: 打印机驱动程序隔离通过使打印机驱动程序可以在与打印后台处理程序运行的进程分离的进程中运行，从而提高了 Windows 打印服务的可靠性。
ms.assetid: b0f11b3f-92f7-41f6-8edb-63b5651f5499
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54dda102a57d0abcd308d881f10d18f6ce336d63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840438"
---
# <a name="printer-driver-isolation"></a>打印机驱动程序隔离


打印机驱动程序隔离通过使打印机驱动程序可以在与打印后台处理程序运行的进程分离的进程中运行，从而提高了 Windows 打印服务的可靠性。

在 Windows 7、Windows Server 2008 R2 和更高版本的操作系统中实现对打印机驱动程序隔离的支持。

对于 Windows 7 和 Windows Server 2008 R2，收件箱打印机驱动程序必须支持打印机驱动程序隔离，并且能够在隔离的进程中运行。

### <a href="" id="previous-versions-of-windows"></a>以前版本的 Windows

在以前版本的 Windows （包括 Windows Server 2008）中，打印机驱动程序始终在与后台处理程序相同的进程中运行。 在后台处理程序进程中运行的打印机驱动程序组件包括以下各项：

-   打印驱动程序配置模块

-   打印处理器

-   呈现模块

单个打印驱动程序组件失败可能导致打印子系统失败，并停止所有用户和所有打印组件的打印操作。

### <a href="" id="new-versions-of-windows"></a>新版本的 Windows

使用 Windows 7 和 Windows Server 2008 R2，管理员可以选择将打印机驱动程序配置为在隔离的进程中运行，这是一个独立于后台处理程序进程的进程。 通过隔离该驱动程序，管理员可防止驱动程序组件中的错误导致打印服务停止。

有关后台处理程序功能的详细信息，请参阅[后台处理程序组件函数和结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)。

### <a href="" id="driver-isolation-support-in-inf-files"></a>INF 文件中的驱动程序隔离支持

默认情况下，如果安装打印机驱动程序的 INF 文件不指示驱动程序支持驱动程序隔离，则 printer 类安装程序会将该驱动程序配置为在后台处理程序进程中运行。 但是，如果 INF 文件指示驱动程序支持驱动程序隔离，则安装程序会将该驱动程序配置为在隔离的进程中运行。 管理员可以覆盖这些配置设置，并为每个驱动程序指定是在后台处理程序进程中还是在隔离的进程中运行该驱动程序。

若要支持驱动程序隔离，安装打印机驱动程序的 INF 文件可以使用**DriverIsolation**关键字来指示驱动程序是否支持打印机驱动程序隔离。 设置**DriverIsolation**= 2 表示驱动程序支持驱动程序隔离。 设置**DriverIsolation**= 0 表示驱动程序不支持驱动程序隔离。 省略 INF 文件中的**DriverIsolation**关键字与设置**DriverIsolation**= 0 的效果相同。

### <a href="" id="spooler-functions-for-driver-isolation-settings"></a>驱动程序隔离设置的后台处理程序功能

下表显示管理员可用于配置驱动程序隔离设置的后台处理程序函数。

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
<td><p>枚举打印机的驱动程序隔离设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=135634" data-raw-source="[FindFirstPrinterChangeNotification](https://go.microsoft.com/fwlink/p/?linkid=135634)">FindFirstPrinterChangeNotification</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=135635" data-raw-source="[FindNextPrinterChangeNotification](https://go.microsoft.com/fwlink/p/?linkid=135635)">FindNextPrinterChangeNotification</a></p></td>
<td><p>请求通知对打印机的驱动程序隔离设置的更改。</p></td>
</tr>
</tbody>
</table>

 

数据的格式如下所示：

-   每个组中的驱动程序由 "\\" 分隔
-   每个驱动程序组由 "\\\\" 分隔

第一组将驱动程序加载到后台处理程序。 每个后续组每个组在隔离的进程中加载驱动程序。 第二个组被视为 "共享" 组，默认情况下会加载其他支持隔离的驱动程序。

### <a href="" id="configuring-driver-isolation-mode-through-administration"></a>通过管理配置驱动程序隔离模式

计算机管理员可以使用 Windows 打印管理控制台或调用 Windows 后台处理程序功能为计算机上安装的每个打印机驱动程序配置驱动程序隔离设置。 管理员将驱动程序配置为使用下表中列出的设置之一。

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
<td><p>在与其他打印机驱动程序共享但独立于后台处理程序进程的进程中运行该驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>隔离</p></td>
<td><p>在独立于后台处理程序进程的进程中运行该驱动程序，并且不与其他打印机驱动程序共享。</p></td>
</tr>
<tr class="odd">
<td><p>无</p></td>
<td><p>在后台处理程序进程中运行该驱动程序。</p></td>
</tr>
</tbody>
</table>

 

理想情况下，打印机驱动程序可以在共享模式下运行。 也就是说，它在与其他打印机驱动程序共享的独立进程中运行，但独立于后台处理程序进程。 如果某个驱动程序可以在独立于后台处理程序进程的进程中运行，则它可能需要在隔离模式下运行，但难以与其他驱动程序共享该进程。 例如，设计良好的驱动程序可能具有与相关驱动程序或同一驱动程序的不同版本冲突的文件名，或驱动程序可能经常出现故障，或者存在与在中运行的其他驱动程序操作冲突的内存泄漏。相同的过程。

为了支持故障排除，域管理员可以在域中的计算机上禁用驱动程序隔离功能，或管理员可以强制计算机上的所有打印机驱动程序在隔离模式下运行。 在隔离模式下，每个驱动程序都必须在独立于后台处理程序和其他打印机驱动程序的进程中运行。

如果组策略禁用了驱动程序隔离，则所有打印机驱动程序的隔离都处于关闭状态。 如果启用了隔离，则各个驱动程序都是模式检查。 如果驱动程序设置了隔离模式，则该驱动程序将根据注册表项在共享、隔离或无模式下运行。 但是，如果驱动程序没有设置隔离模式，并且它与隔离兼容，则会在共享模式下运行。 如果驱动程序与模式不兼容，则组策略重写将确定驱动程序是以共享模式还是无模式运行。

下图显示了选择驱动程序隔离模式的决策图：

![选择驱动程序隔离模式的流程图](images/isolation.png)

### <a name="spooler-functions-allowed-under-driver-isolation"></a>驱动程序隔离下允许使用后台处理程序函数

驱动程序隔离下只允许特定的函数。

### <a href="" id="spoolss-dll-functions"></a>Spoolss 函数

以下函数由 spoolss 导出，并通过链接到 spoolss 可用于后台处理程序插件。

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

### <a href="" id="winspool-drv-functions"></a>Winspool.drv. winspool.drv 函数

以下函数由 winspool.drv 导出，并通过链接到 Winspool.drv 可用于后台处理程序插件。

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

 

 




