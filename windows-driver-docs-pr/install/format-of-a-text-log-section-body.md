---
title: 文本日志部分正文的格式
description: 文本日志部分正文的格式
keywords:
- 节体 WDK Setupapi.log
- 格式化 WDK Setupapi.log 日志记录
- 文本日志 WDK Setupapi.log，部分正文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d893d44019c6c0371d4cc492478bf3b7c3c58907
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820181"
---
# <a name="format-of-a-text-log-section-body"></a>文本日志部分正文的格式


*文本日志节正文* 包含零个或多个应用于与文本日志部分关联的操作的日志项。 节体日志条目的格式包括 *entry_prefix* 字段、 *time_stamp* 字段、 *event_category* 字段、 *缩进* 字段和 *formatted_message* 字段，如下所示：

*event_category 缩进 time_stamp entry_prefix formatted_message*

部分正文日志条目的最大长度（以字符为336）。

<a href="" id="entry-prefix-field"></a>*entry_prefix* 字段  
指示日志条目是否为错误消息、警告消息或信息消息。 " *Entry_prefix* " 字段始终存在，其中包含下表中列出的字符串之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>Entry_prefix</em> 字段</th>
<th align="left">消息类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"!!!  "</code></pre></td>
<td align="left"><p>错误消息</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"!    "</code></pre></td>
<td align="left"><p>警告消息</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"     "</code></pre></td>
<td align="left"><p>除错误消息或警告消息以外的信息消息</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="time-stamp-field"></a>*time_stamp* 字段  
指示发生日志事件的系统时间。 *Time_stamp* 字段是可选的，默认情况下，setupapi.log 不包含时间戳。 不过， [**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog) 支持在日志条目中包含时间戳。 *Time_stamp* 字段的格式与 [文本日志节标题格式](format-of-a-text-log-section-header.md)中描述的 *time_stamp* 字段的格式相同。

<a href="" id="event-category-field"></a>*event_category* 字段  
指示执行日志条目的 Setupapi.log 操作的类别。 *Event_category* 字段通常存在，但不是必需的。 如果 *event_category* 字段存在，它将包含下表中列出的字符串之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>Event_category</em> 字段字符串</th>
<th align="left">Setupapi.log 操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"...: "</code></pre></td>
<td align="left"><p>供应商提供的操作</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"bak: "</code></pre></td>
<td align="left"><p>备份数据</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"cci: "</code></pre></td>
<td align="left"><p>类安装程序或共同安装程序操作</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"cpy: "</code></pre></td>
<td align="left"><p>复制文件</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"dvi: "</code></pre></td>
<td align="left"><p>设备安装</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"flq: "</code></pre></td>
<td align="left"><p>管理文件队列</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"inf: "</code></pre></td>
<td align="left"><p>管理 INF 文件</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"ndv: "</code></pre></td>
<td align="left"><p>新建设备向导</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"prp: "</code></pre></td>
<td align="left"><p>管理设备和驱动程序属性</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"reg: "</code></pre></td>
<td align="left"><p>管理注册表设置</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"set: "</code></pre></td>
<td align="left"><p>常规设置</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"sig: "</code></pre></td>
<td align="left"><p>验证数字签名</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"sto: "</code></pre></td>
<td align="left"><p>管理驱动程序存储</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"ui : "</code></pre></td>
<td align="left"><p>"管理用户界面" 对话框</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"ump: "</code></pre></td>
<td align="left"><p>用户模式 PnP 管理器</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="indentation-field"></a>*缩进* 字段  
由零个或多个 *缩进单位* 的序列组成，其中，缩进单位为包含五个空格的等宽字符串。 *缩进* 字段是可选的，默认情况下 setupapi.log 不包括缩进。 **SetupWriteTextLog** 支持更改日志条目中包含的缩进单位数。

<a href="" id="formatted-message-field"></a>*formatted_message* 字段  
包含适用于日志条目的特定信息。

记录的节正文项取决于为日志设置的事件级别以及为日志启用的类别级别。 有关这些设置的详细信息，请参阅 [Setupapi.log 日志记录注册表设置](setupapi-logging-registry-settings.md)。

当 Setupapi.log 创建对应用到设备安装的操作进行分组的部分时，它还会以递归方式将节中的主体日志条目分组。 Setupapi.log 通过批注和缩进日志条目的方式区分子节。 下面的部分摘自典型的设备安装部分。 子节以日志条目 "dvi： {构建驱动程序列表}" 开头，以日志条目 "dvi： {Build Driver List-exit (0x00000000) }" 结尾。 此子节显示了一系列典型的日志条目，其中包括 *entry_prefix*、 *event_category*、 *缩进* 和 *formatted_message* 字段。 编写日志项的 Setupapi.log 操作还会创建缩进，并提供带格式消息的内容。 此示例的事件级别已设置为 TXTLOG_DETAILS 并为此示例启用了所有类别级别。

```cpp
>>>  [Device Install - PCI\VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00\3&61aaa01&0&38]
>>>  2005/02/13 22:06:28.109: Section start
...
 Deleted section body log entries
...
     dvi: {Build Driver List}
     dvi:      Enumerating all INFs...
     dvi:      Found driver match:
     dvi:           HardwareID - PCI\VEN_104C&DEV_8019
     dvi:           InfName    - C:\WINDOWS\inf\1394.inf
     dvi:           DevDesc    - Texas Instruments OHCI Compliant IEEE 1394 Host Controller
     dvi:           DrvDesc    - Texas Instruments OHCI Compliant IEEE 1394 Host Controller
     dvi:           Provider   - Microsoft
     dvi:           Mfg        - Texas Instruments
     dvi:           InstallSec - TIOHCI_Install
     dvi:           ActualSec  - TIOHCI_Install.NT
 dvi:           Rank       - 0x00002001
     dvi:           DrvDate    - 10/01/2002
 dvi:           Version    - 6.0.5033.0 
!!!  inf:      InfCache: Error flagging 1394.inf for match string pci\ven_104c&dev_8019
     dvi: {Build Driver List - exit(0x00000000)}
...
 Deleted section body log entries 
...
<<<  [2005/02/13 22:06:29.000: Section end]
<<<  [Exit Status(0x00000000)]
```

 

