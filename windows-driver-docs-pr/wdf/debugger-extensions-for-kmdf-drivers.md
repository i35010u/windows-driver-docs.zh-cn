---
title: Wdfkd.dll 中的调试程序扩展摘要
description: Windows 驱动程序工具包 (WDK) 包含一个名为 Wdfkd.dll 的调试器扩展库。
keywords:
- 扩展 WDK 调试器
- 调试器扩展 WDK KMDF
- 调试驱动程序 WDK KMDF、调试器扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28020db9f021088853430c30a0320fbc77dea2ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837039"
---
#  <a name="summary-of-debugger-extensions-in-wdfkddll"></a>Wdfkd.dll 中的调试程序扩展摘要


Windows 驱动程序工具包 (WDK) 包含一个名为 *Wdfkd.dll* 的调试器扩展库。 此库包含调试程序扩展命令，可用于调试 Kernel-Mode Driver Framework (KMDF) ，以及从版本2开始的 User-Mode 驱动程序框架 (UMDF) 驱动程序。

有关每个命令的完整说明，请参阅 [**Windows Driver Framework extension ( # A0)**](../debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-.md)。 有关所有可用调试器扩展库的详细信息，请参阅 [Windows 调试](../debugger/index.md) 包附带的文档。

可以在视频中找到演示如何调试 KMDF 驱动程序的视频系列 [：调试 KMDF 驱动程序](debugging-kernel-mode-driver-framework-drivers.md)。

若要调试使用 UMDF 1.11 版或更早版本的驱动程序，必须改用 *Wudfext.dll* 调试程序扩展库。 有关详细信息，请参阅 [用户模式驱动程序框架扩展 ( # A0) ](../debugger/user-mode-driver-framework-extensions--wudfext-dll-.md)。

*Wdfkd.dll* 扩展库提供的扩展命令包括：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">分机</th>
<th align="left">说明</th>
<th align="left">框架</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfhelp" data-raw-source="[&lt;strong&gt;!wdfkd.wdfhelp&lt;/strong&gt;](../debugger/-wdfkd-wdfhelp.md)"><strong>!wdfkd.wdfhelp</strong></a></p></td>
<td align="left"><p>显示此调试器扩展列表。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfchildlist" data-raw-source="[&lt;strong&gt;!wdfkd.wdfchildlist&lt;/strong&gt;](../debugger/-wdfkd-wdfchildlist.md)"><strong>!wdfkd.wdfchildlist</strong></a></p></td>
<td align="left"><p>显示子列表的状态，以及有关子列表中所有设备标识说明的信息。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfcollection" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcollection&lt;/strong&gt;](../debugger/-wdfkd-wdfcollection.md)"><strong>!wdfkd.wdfcollection</strong></a></p></td>
<td align="left"><p>显示集合中包含的对象。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfcommonbuffer" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcommonbuffer&lt;/strong&gt;](../debugger/-wdfkd-wdfcommonbuffer.md)"><strong>!wdfkd.wdfcommonbuffer</strong></a></p></td>
<td align="left"><p>显示有关 <a href="using-common-buffers.md" data-raw-source="[common buffer object](using-common-buffers.md)">公用缓冲区对象</a>的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfcrashdump" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcrashdump&lt;/strong&gt;](../debugger/-wdfkd-wdfcrashdump.md)"><strong>!wdfkd.wdfcrashdump</strong></a></p></td>
<td align="left"><p>显示框架的事件日志记录（如果可用），该记录来自小内存转储。 如果在注册表中设置了 <a href="registry-values-for-debugging-kmdf-drivers.md" data-raw-source="[ForceLogsInMiniDump](registry-values-for-debugging-kmdf-drivers.md)">ForceLogsInMiniDump</a> ，或者框架可以确定你的驱动程序导致了错误检查，则可以使用框架的事件日志记录。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfdevext" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevext&lt;/strong&gt;](../debugger/-wdfkd-wdfdevext.md)"><strong>!wdfkd.wdfdevext</strong></a></p></td>
<td align="left"><p>显示与 Microsoft Windows 驱动模型 (WDM) <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object" data-raw-source="[&lt;strong&gt;DEVICE_OBJECT&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)"><strong>DEVICE_OBJECT</strong></a>结构的<strong>DeviceExtension</strong>成员关联的 WDFDEVICE 类型的对象句柄。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 1</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfdevice" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevice&lt;/strong&gt;](../debugger/-wdfkd-wdfdevice.md)"><strong>!wdfkd.wdfdevice</strong></a></p></td>
<td align="left"><p>显示与 WDFDEVICE 类型的句柄关联的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfdeviceinterrupts" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdeviceinterrupts&lt;/strong&gt;](../debugger/-wdfkd-wdfdeviceinterrupts.md)"><strong>!wdfkd.wdfdeviceinterrupts</strong></a></p></td>
<td align="left"><p>显示指定设备句柄的所有中断对象</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfdevicequeues" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevicequeues&lt;/strong&gt;](../debugger/-wdfkd-wdfdevicequeues.md)"><strong>!wdfkd.wdfdevicequeues</strong></a></p></td>
<td align="left"><p>显示属于指定设备的所有队列对象的相关信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenabler" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmaenabler&lt;/strong&gt;](../debugger/-wdfkd-wdfdmaenabler.md)"><strong>!wdfkd.wdfdmaenabler</strong></a></p></td>
<td align="left"><p>显示有关 <a href="framework-dma-objects.md" data-raw-source="[DMA enabler object](framework-dma-objects.md)">dma 启用程序对象</a>及其关联的 dma 事务对象和公共缓冲区对象的信息。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenablers" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmaenablers&lt;/strong&gt;](../debugger/-wdfkd-wdfdmaenablers.md)"><strong>!wdfkd.wdfdmaenablers</strong></a></p></td>
<td align="left"><p>显示与指定的设备对象关联的所有 DMA 启用程序对象、DMA 事务对象和公共缓冲区对象的摘要。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfdmatransaction" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmatransaction&lt;/strong&gt;](../debugger/-wdfkd-wdfdmatransaction.md)"><strong>!wdfkd.wdfdmatransaction</strong></a></p></td>
<td align="left"><p>显示 (DMA) transaction 对象的 WDF 直接内存访问的相关信息。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdriverinfo&lt;/strong&gt;](../debugger/-wdfkd-wdfdriverinfo.md)"><strong>!wdfkd.wdfdriverinfo</strong></a></p></td>
<td align="left"><p>显示有关基于框架的驱动程序的信息，如其库版本和对象句柄的层次结构。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfextendwatchdog" data-raw-source="[&lt;strong&gt;!wdfkd.wdfextendwatchdog&lt;/strong&gt;](../debugger/-wdfkd-wdfextendwatchdog.md)"><strong>!wdfkd.wdfextendwatchdog</strong></a></p></td>
<td align="left"><p>扩展了在电源转换期间 (从10分钟到24小时) 框架监视程序计时器的超时时间。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdffindobjects" data-raw-source="[&lt;strong&gt;!wdfkd.wdffindobjects&lt;/strong&gt;](../debugger/-wdfkd-wdffindobjects.md)"><strong>!wdfkd.wdffindobjects</strong></a></p></td>
<td align="left"><p>查找并显示框架对象。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfforwardprogress" data-raw-source="[&lt;strong&gt;!wdfkd.wdfforwardprogress&lt;/strong&gt;](../debugger/-wdfkd-wdfforwardprogress.md)"><strong>!wdfkd.wdfforwardprogress</strong></a></p></td>
<td align="left"><p>显示有关 i/o 队列的 <a href="guaranteeing-forward-progress-of-i-o-operations.md" data-raw-source="[guaranteed forward progress](guaranteeing-forward-progress-of-i-o-operations.md)">保证前进进度</a> 功能的信息。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfgetdriver" data-raw-source="[&lt;strong&gt;!wdfkd.wdfgetdriver&lt;/strong&gt;](../debugger/-wdfkd-wdfgetdriver.md)"><strong>!wdfkd.wdfgetdriver</strong></a></p></td>
<td align="left"><p>显示驱动程序名称。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfhandle" data-raw-source="[&lt;strong&gt;!wdfkd.wdfhandle&lt;/strong&gt;](../debugger/-wdfkd-wdfhandle.md)"><strong>!wdfkd.wdfhandle</strong></a></p></td>
<td align="left"><p>显示有关框架对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfinterrupt" data-raw-source="[&lt;strong&gt;!wdfkd.wdfinterrupt&lt;/strong&gt;](../debugger/-wdfkd-wdfinterrupt.md)"><strong>!wdfkd.wdfinterrupt</strong></a></p></td>
<td align="left"><p>显示有关框架中断对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfiotarget" data-raw-source="[&lt;strong&gt;!wdfkd.wdfiotarget&lt;/strong&gt;](../debugger/-wdfkd-wdfiotarget.md)"><strong>!wdfkd.wdfiotarget</strong></a></p></td>
<td align="left"><p>显示有关 WDFIOTARGET 类型化对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfldr" data-raw-source="[&lt;strong&gt;!wdfkd.wdfldr&lt;/strong&gt;](../debugger/-wdfkd-wdfldr.md)"><strong>!wdfkd.wdfldr</strong></a></p></td>
<td align="left"><p>显示有关使用框架库的所有驱动程序的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 1</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdflogdump" data-raw-source="[&lt;strong&gt;!wdfkd.wdflogdump&lt;/strong&gt;](../debugger/-wdfkd-wdflogdump.md)"><strong>!wdfkd.wdflogdump</strong></a></p></td>
<td align="left"><p>显示框架的事件日志记录（如果可用），从完整内存转储、内核内存转储或实时内核模式目标。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdflogsave" data-raw-source="[&lt;strong&gt;!wdfkd.wdflogsave&lt;/strong&gt;](../debugger/-wdfkd-wdflogsave.md)"><strong>!wdfkd.wdflogsave</strong></a></p></td>
<td align="left"><p>将框架的事件日志记录保存在事件跟踪日志 ( 中。<em>etl</em>) 文件，你可以使用 <a href="/windows-hardware/drivers/devtest/traceview" data-raw-source="[TraceView](../devtest/traceview.md)">TraceView</a>来查看此文件。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfmemory" data-raw-source="[&lt;strong&gt;!wdfkd.wdfmemory&lt;/strong&gt;](../debugger/-wdfkd-wdfmemory.md)"><strong>!wdfkd.wdfmemory</strong></a></p></td>
<td align="left"><p>显示内存对象的缓冲区地址和大小。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfobject" data-raw-source="[&lt;strong&gt;!wdfkd.wdfobject&lt;/strong&gt;](../debugger/-wdfkd-wdfobject.md)"><strong>!wdfkd.wdfobject</strong></a></p></td>
<td align="left"><p>显示有关框架对象的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfopenhandles" data-raw-source="[&lt;strong&gt;!wdfkd.wdfopenhandles&lt;/strong&gt;](../debugger/-wdfkd-wdfopenhandles.md)"><strong>!wdfkd.wdfopenhandles</strong></a></p></td>
<td align="left"><p>显示有关在指定的 WDF 设备上打开的所有句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfpoolusage" data-raw-source="[&lt;strong&gt;!wdfkd.wdfpoolusage&lt;/strong&gt;](../debugger/-wdfkd-wdfpoolusage.md)"><strong>!wdfkd.wdfpoolusage</strong></a></p></td>
<td align="left"><p>显示驱动程序的内存池使用情况。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfqueue" data-raw-source="[&lt;strong&gt;!wdfkd.wdfqueue&lt;/strong&gt;](../debugger/-wdfkd-wdfqueue.md)"><strong>!wdfkd.wdfqueue</strong></a></p></td>
<td align="left"><p>显示有关 WDFQUEUE 类型化对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfrequest" data-raw-source="[&lt;strong&gt;!wdfkd.wdfrequest&lt;/strong&gt;](../debugger/-wdfkd-wdfrequest.md)"><strong>!wdfkd.wdfrequest</strong></a></p></td>
<td align="left"><p>显示有关 WDFREQUEST 类型化对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfsearchpath" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsearchpath&lt;/strong&gt;](../debugger/-wdfkd-wdfsearchpath.md)"><strong>!wdfkd.wdfsearchpath</strong></a></p></td>
<td align="left"><p>设置用于查找框架日志格式文件的搜索路径。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfsettraceprefix" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsettraceprefix&lt;/strong&gt;](../debugger/-wdfkd-wdfsettraceprefix.md)"><strong>!wdfkd.wdfsettraceprefix</strong></a></p></td>
<td align="left"><p>设置用于跟踪框架事件日志中的消息的前缀字符串。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfsetdriver" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsetdriver&lt;/strong&gt;](../debugger/-wdfkd-wdfsetdriver.md)"><strong>!wdfkd.wdfsetdriver</strong></a></p></td>
<td align="left"><p>为需要驱动程序名称的其他命令设置用作默认名称的驱动程序名称。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfspinlock" data-raw-source="[&lt;strong&gt;!wdfkd.wdfspinlock&lt;/strong&gt;](../debugger/-wdfkd-wdfspinlock.md)"><strong>!wdfkd.wdfspinlock</strong></a></p></td>
<td align="left"><p>显示有关框架旋转锁定对象的信息。 此信息包括自旋锁的获取历史记录以及持有锁的时间长度。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker" data-raw-source="[&lt;strong&gt;!wdfkd.wdftagtracker&lt;/strong&gt;](../debugger/-wdfkd-wdftagtracker.md)"><strong>!wdfkd.wdftagtracker</strong></a></p></td>
<td align="left"><p>显示标记信息 (包括指定对象标记的标记值、行、文件和时间) 。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdftmffile" data-raw-source="[&lt;strong&gt;!wdfkd.wdftmffile&lt;/strong&gt;](../debugger/-wdfkd-wdftmffile.md)"><strong>!wdfkd.wdftmffile</strong></a></p></td>
<td align="left"><p>指定 ( 的跟踪消息格式。<em>tmf</em>) <strong>！ wdflogdump</strong> 扩展将用于显示事件日志记录的文件。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdftraceprtdebug" data-raw-source="[&lt;strong&gt;!wdfkd.wdftraceprtdebug&lt;/strong&gt;](../debugger/-wdfkd-wdftraceprtdebug.md)"><strong>!wdfkd.wdftraceprtdebug</strong></a></p></td>
<td align="left"><p>打开 TracePrt 诊断模式。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstack" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdevstack&lt;/strong&gt;](../debugger/-wdfkd-wdfumdevstack.md)"><strong>!wdfkd.wdfumdevstack</strong></a></p></td>
<td align="left"><p>在隐式进程中显示有关 UMDF 设备堆栈的详细信息。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstacks" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdevstacks&lt;/strong&gt;](../debugger/-wdfkd-wdfumdevstacks.md)"><strong>!wdfkd.wdfumdevstacks</strong></a></p></td>
<td align="left"><p>在隐式进程中显示有关所有 UMDF 设备堆栈的信息。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfumdownirp" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdownirp&lt;/strong&gt;](../debugger/-wdfkd-wdfumdownirp.md)"><strong>!wdfkd.wdfumdownirp</strong></a></p></td>
<td align="left"><p>显示与指定的用户模式 IRP 关联的内核模式 i/o 请求数据包 (IRP) 。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfumfile" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumfile&lt;/strong&gt;](../debugger/-wdfkd-wdfumfile.md)"><strong>!wdfkd.wdfumfile</strong></a></p></td>
<td align="left"><p>显示有关 UMDF 堆栈内文件的信息。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfumirp" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumirp&lt;/strong&gt;](../debugger/-wdfkd-wdfumirp.md)"><strong>!wdfkd.wdfumirp</strong></a></p></td>
<td align="left"><p>显示有关用户模式 i/o 请求数据包 (UM IRP) 的信息。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfumirps" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumirps&lt;/strong&gt;](../debugger/-wdfkd-wdfumirps.md)"><strong>!wdfkd.wdfumirps</strong></a></p></td>
<td align="left"><p>显示隐式进程中 (UM Irp) 挂起的用户模式 i/o 请求包的列表。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfusbdevice" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbdevice&lt;/strong&gt;](../debugger/-wdfkd-wdfusbdevice.md)"><strong>!wdfkd.wdfusbdevice</strong></a></p></td>
<td align="left"><p>显示有关 WDFUSBDEVICE 类型化对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfusbinterface" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbinterface&lt;/strong&gt;](../debugger/-wdfkd-wdfusbinterface.md)"><strong>!wdfkd.wdfusbinterface</strong></a></p></td>
<td align="left"><p>显示有关 WDFUSBINTERFACE 类型化对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfusbpipe" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbpipe&lt;/strong&gt;](../debugger/-wdfkd-wdfusbpipe.md)"><strong>!wdfkd.wdfusbpipe</strong></a></p></td>
<td align="left"><p>显示有关 WDFUSBPIPE 类型化对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/debugger/-wdfkd-wdfwmi" data-raw-source="[&lt;strong&gt;!wdfkd.wdfwmi&lt;/strong&gt;](../debugger/-wdfkd-wdfwmi.md)"><strong>!wdfkd.wdfwmi</strong></a></p></td>
<td align="left"><p>显示 WMI) 信息 (设备的 Windows Management Instrumentation。</p></td>
<td align="left">KMDF</td>
</tr>
</tbody>
</table>

 

