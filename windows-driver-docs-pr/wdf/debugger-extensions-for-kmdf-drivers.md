---
title: Wdfkd.dll 中的调试程序扩展摘要
description: Windows Driver Kit (WDK) 包括名为 Wdfkd.dll 的调试器扩展库。
ms.assetid: 5a83ea58-5dbf-40a6-b4cb-9c330851fc33
keywords:
- 扩展 WDK 调试器
- 调试器扩展 WDK KMDF
- 调试驱动程序 WDK KMDF，调试器扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a8312da48be5f01f540c50ed1aa1c0d29825172
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392696"
---
#  <a name="summary-of-debugger-extensions-in-wdfkddll"></a>Wdfkd.dll 中的调试程序扩展摘要


Windows Driver Kit (WDK) 包括调试器扩展库，名为*Wdfkd.dll*。 此库包含可用于调试从版本 2 开始的内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 驱动程序的调试程序扩展命令。

每个命令的完整说明，请参阅[ **Windows 驱动程序框架扩展 (Wdfkd.dll)**](https://msdn.microsoft.com/library/windows/hardware/ff551876)。 有关所有可用的调试器扩展库的详细信息，请参阅随提供的文档[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)包。

您可以找到一个演示如何调试在 KMDF 驱动程序的视频系列[视频：调试 KMDF 驱动程序](debugging-kernel-mode-driver-framework-drivers.md)。

若要调试使用 UMDF 版本 1.11 或更早版本的驱动程序，您必须改用*Wudfext.dll*调试器扩展库。 有关详细信息，请参阅[用户模式驱动程序框架扩展 (Wudfext.dll)](https://msdn.microsoft.com/library/windows/hardware/ff560030)。

扩展命令*Wdfkd.dll*扩展库提供了包括：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">扩展</th>
<th align="left">描述</th>
<th align="left">框架</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565761" data-raw-source="[&lt;strong&gt;!wdfkd.wdfhelp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565761)"><strong>!wdfkd.wdfhelp</strong></a></p></td>
<td align="left"><p>显示调试器扩展此列表。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565672" data-raw-source="[&lt;strong&gt;!wdfkd.wdfchildlist&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565672)"><strong>!wdfkd.wdfchildlist</strong></a></p></td>
<td align="left"><p>显示子列表的状态和所有子列表中的设备标识说明信息。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565675" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcollection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565675)"><strong>!wdfkd.wdfcollection</strong></a></p></td>
<td align="left"><p>显示集合中包含的对象。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565679" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcommonbuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565679)"><strong>!wdfkd.wdfcommonbuffer</strong></a></p></td>
<td align="left"><p>显示有关的信息<a href="using-common-buffers.md" data-raw-source="[common buffer object](using-common-buffers.md)">常见缓冲区对象</a>。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565682" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcrashdump&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565682)"><strong>!wdfkd.wdfcrashdump</strong></a></p></td>
<td align="left"><p>显示框架的事件日志记录，如果可用，从很小的内存转储。 框架的事件日志记录可如果<a href="registry-values-for-debugging-kmdf-drivers.md" data-raw-source="[ForceLogsInMiniDump](registry-values-for-debugging-kmdf-drivers.md)">ForceLogsInMiniDump</a>设置在注册表中，或如果框架可以确定您的驱动程序导致的 bug 检查。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565686" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565686)"><strong>!wdfkd.wdfdevext</strong></a></p></td>
<td align="left"><p>显示与之关联的 WDFDEVICE 类型对象句柄<strong>DeviceExtension</strong>成员的 Microsoft Windows 驱动程序模型 (WDM) <a href="https://msdn.microsoft.com/library/windows/hardware/ff543147" data-raw-source="[&lt;strong&gt;DEVICE_OBJECT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543147)"> <strong>DEVICE_OBJECT</strong> </a>结构。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 1</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565703" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565703)"><strong>!wdfkd.wdfdevice</strong></a></p></td>
<td align="left"><p>显示与 WDFDEVICE 类型句柄关联的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265378" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdeviceinterrupts&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265378)"><strong>!wdfkd.wdfdeviceinterrupts</strong></a></p></td>
<td align="left"><p>显示指定的设备句柄的所有中断对象</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565715" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevicequeues&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565715)"><strong>!wdfkd.wdfdevicequeues</strong></a></p></td>
<td align="left"><p>显示有关属于指定设备的队列对象的所有信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565717" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmaenabler&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565717)"><strong>!wdfkd.wdfdmaenabler</strong></a></p></td>
<td align="left"><p>显示有关的信息<a href="framework-dma-objects.md" data-raw-source="[DMA enabler object](framework-dma-objects.md)">DMA 促成因素对象</a>，以及其关联的 DMA 事务对象和常用的缓冲区对象。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565719" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmaenablers&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565719)"><strong>!wdfkd.wdfdmaenablers</strong></a></p></td>
<td align="left"><p>显示所有 DMA 启用程序对象、 DMA 事务对象和公共与指定的设备对象相关联的缓冲区对象的摘要。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565721" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmatransaction&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565721)"><strong>!wdfkd.wdfdmatransaction</strong></a></p></td>
<td align="left"><p>显示有关 WDF 直接内存访问 (DMA) 事务对象的信息。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565724" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdriverinfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565724)"><strong>!wdfkd.wdfdriverinfo</strong></a></p></td>
<td align="left"><p>显示基于 framework 的驱动程序的信息，例如，其库版本和层次结构的对象句柄。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565731" data-raw-source="[&lt;strong&gt;!wdfkd.wdfextendwatchdog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565731)"><strong>!wdfkd.wdfextendwatchdog</strong></a></p></td>
<td align="left"><p>扩展了超时期限 （从 10 分钟到 24 小时） 的框架的监视程序计时器 power 转换期间。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565738" data-raw-source="[&lt;strong&gt;!wdfkd.wdffindobjects&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565738)"><strong>!wdfkd.wdffindobjects</strong></a></p></td>
<td align="left"><p>查找并显示 framework 对象。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565743" data-raw-source="[&lt;strong&gt;!wdfkd.wdfforwardprogress&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565743)"><strong>!wdfkd.wdfforwardprogress</strong></a></p></td>
<td align="left"><p>显示有关的信息<a href="guaranteeing-forward-progress-of-i-o-operations.md" data-raw-source="[guaranteed forward progress](guaranteeing-forward-progress-of-i-o-operations.md)">保证向前推进</a>的 I/O 队列功能。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565751" data-raw-source="[&lt;strong&gt;!wdfkd.wdfgetdriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565751)"><strong>!wdfkd.wdfgetdriver</strong></a></p></td>
<td align="left"><p>显示驱动程序名称。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565758" data-raw-source="[&lt;strong&gt;!wdfkd.wdfhandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565758)"><strong>!wdfkd.wdfhandle</strong></a></p></td>
<td align="left"><p>显示有关 framework 对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565787" data-raw-source="[&lt;strong&gt;!wdfkd.wdfinterrupt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565787)"><strong>!wdfkd.wdfinterrupt</strong></a></p></td>
<td align="left"><p>显示有关 framework 中断对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565791" data-raw-source="[&lt;strong&gt;!wdfkd.wdfiotarget&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565791)"><strong>!wdfkd.wdfiotarget</strong></a></p></td>
<td align="left"><p>显示有关 WDFIOTARGET 类型对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565803" data-raw-source="[&lt;strong&gt;!wdfkd.wdfldr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565803)"><strong>!wdfkd.wdfldr</strong></a></p></td>
<td align="left"><p>显示有关正在使用框架库的驱动程序的所有信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 1</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565805" data-raw-source="[&lt;strong&gt;!wdfkd.wdflogdump&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565805)"><strong>!wdfkd.wdflogdump</strong></a></p></td>
<td align="left"><p>显示框架的事件日志记录，如果可用，从完全内存转储、 内核内存转储或实时的内核模式目标。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566102" data-raw-source="[&lt;strong&gt;!wdfkd.wdflogsave&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566102)"><strong>!wdfkd.wdflogsave</strong></a></p></td>
<td align="left"><p>将框架的事件日志记录保存在事件跟踪日志 (。<em>etl</em>) 文件，您可以通过使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff553872" data-raw-source="[TraceView](https://msdn.microsoft.com/library/windows/hardware/ff553872)">TraceView</a>。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566103" data-raw-source="[&lt;strong&gt;!wdfkd.wdfmemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566103)"><strong>!wdfkd.wdfmemory</strong></a></p></td>
<td align="left"><p>显示内存对象的缓冲区地址和大小。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566107" data-raw-source="[&lt;strong&gt;!wdfkd.wdfobject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566107)"><strong>!wdfkd.wdfobject</strong></a></p></td>
<td align="left"><p>显示有关 framework 对象的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566110" data-raw-source="[&lt;strong&gt;!wdfkd.wdfopenhandles&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566110)"><strong>!wdfkd.wdfopenhandles</strong></a></p></td>
<td align="left"><p>显示有关指定 WDF 设备打开的所有句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566115" data-raw-source="[&lt;strong&gt;!wdfkd.wdfpoolusage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566115)"><strong>!wdfkd.wdfpoolusage</strong></a></p></td>
<td align="left"><p>显示驱动程序的内存池使用情况。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566118" data-raw-source="[&lt;strong&gt;!wdfkd.wdfqueue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566118)"><strong>!wdfkd.wdfqueue</strong></a></p></td>
<td align="left"><p>显示有关 WDFQUEUE 类型对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566119" data-raw-source="[&lt;strong&gt;!wdfkd.wdfrequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566119)"><strong>!wdfkd.wdfrequest</strong></a></p></td>
<td align="left"><p>显示有关 WDFREQUEST 类型对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566120" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsearchpath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566120)"><strong>!wdfkd.wdfsearchpath</strong></a></p></td>
<td align="left"><p>设置用于查找框架日志格式文件的搜索路径。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566123" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsettraceprefix&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566123)"><strong>!wdfkd.wdfsettraceprefix</strong></a></p></td>
<td align="left"><p>设置框架的事件日志中跟踪消息的前缀字符串。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566121" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsetdriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566121)"><strong>!wdfkd.wdfsetdriver</strong></a></p></td>
<td align="left"><p>设置用作需要驱动程序名称的其他命令的默认名称的驱动程序名称。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566125" data-raw-source="[&lt;strong&gt;!wdfkd.wdfspinlock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566125)"><strong>!wdfkd.wdfspinlock</strong></a></p></td>
<td align="left"><p>显示有关 framework 自旋锁对象的信息。 此信息包括旋转锁获取历史记录和在持有锁定时的时间长度。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566126" data-raw-source="[&lt;strong&gt;!wdfkd.wdftagtracker&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566126)"><strong>!wdfkd.wdftagtracker</strong></a></p></td>
<td align="left"><p>显示指定的对象标记的标记信息 （包括标记值、 行、 文件和时间）。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566128" data-raw-source="[&lt;strong&gt;!wdfkd.wdftmffile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566128)"><strong>!wdfkd.wdftmffile</strong></a></p></td>
<td align="left"><p>指定跟踪消息格式 (。<em>tmf</em>) 的文件<strong>！ wdflogdump</strong>扩展将用来显示事件日志记录。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566129" data-raw-source="[&lt;strong&gt;!wdfkd.wdftraceprtdebug&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566129)"><strong>!wdfkd.wdftraceprtdebug</strong></a></p></td>
<td align="left"><p>打开 TracePrt 诊断模式。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265379" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdevstack&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265379)"><strong>!wdfkd.wdfumdevstack</strong></a></p></td>
<td align="left"><p>显示隐式的过程中的 UMDF 设备堆栈的详细的信息。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265380" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdevstacks&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265380)"><strong>!wdfkd.wdfumdevstacks</strong></a></p></td>
<td align="left"><p>隐式的过程中将显示有关所有 UMDF 设备堆栈的信息。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265381" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdownirp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265381)"><strong>!wdfkd.wdfumdownirp</strong></a></p></td>
<td align="left"><p>显示与指定的用户模式 IRP 相关联的内核模式 I/O 请求数据包 (IRP)。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265382" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumfile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265382)"><strong>!wdfkd.wdfumfile</strong></a></p></td>
<td align="left"><p>显示有关 UMDF 内部堆栈文件的信息。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265383" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumirp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265383)"><strong>!wdfkd.wdfumirp</strong></a></p></td>
<td align="left"><p>显示用户模式下 I/O 请求数据包 (UM IRP) 相关信息。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265384" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumirps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265384)"><strong>!wdfkd.wdfumirps</strong></a></p></td>
<td align="left"><p>显示隐式的过程中挂起用户模式下 I/O 请求数据包 (UM Irp) 的列表。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566131" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbdevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566131)"><strong>!wdfkd.wdfusbdevice</strong></a></p></td>
<td align="left"><p>显示有关 WDFUSBDEVICE 类型对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566134" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbinterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566134)"><strong>!wdfkd.wdfusbinterface</strong></a></p></td>
<td align="left"><p>显示有关 WDFUSBINTERFACE 类型对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566136" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbpipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566136)"><strong>!wdfkd.wdfusbpipe</strong></a></p></td>
<td align="left"><p>显示有关 WDFUSBPIPE 类型对象句柄的信息。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566137" data-raw-source="[&lt;strong&gt;!wdfkd.wdfwmi&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566137)"><strong>!wdfkd.wdfwmi</strong></a></p></td>
<td align="left"><p>显示设备的 Windows Management Instrumentation (WMI) 信息。</p></td>
<td align="left">KMDF</td>
</tr>
</tbody>
</table>

 

 

 





