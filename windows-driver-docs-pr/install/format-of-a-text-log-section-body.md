---
title: 文本日志部分正文的格式
description: 文本日志部分正文的格式
ms.assetid: 37995fc8-9822-4c2f-ba6a-154a86e1eadf
keywords:
- 节正文 WDK SetupAPI
- 格式 WDK SetupAPI 日志记录
- 文本日志 WDK SetupAPI，部分正文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17264b2db9d8bd40913b3a6b02e58eca16097874
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464122"
---
# <a name="format-of-a-text-log-section-body"></a>文本日志部分正文的格式


一个*文本日志部分正文*包含零个或多个日志条目，用于将应用于与文本日志部分相关联的操作。 部分正文日志条目的格式包括*entry_prefix*字段中， *time_stamp*字段中， *event_category*字段中，*缩进*字段中，和一个*formatted_message*字段中，按如下所示：

*entry_prefix time_stamp event_category 缩进 formatted_message*

以字符为单位的部分正文日志条目的最大长度为 336。

<a href="" id="entry-prefix-field"></a>*entry_prefix* field  
指示日志条目是一条错误消息、 警告消息或信息性消息。 *Entry_prefix*字段将始终存在，其中包含下表中列出的字符串之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>Entry_prefix</em>字段</th>
<th align="left">消息类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"!!!  "</code></pre></td>
<td align="left"><p>一条错误消息</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"!    "</code></pre></td>
<td align="left"><p>一条警告消息</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"     "</code></pre></td>
<td align="left"><p>一条错误消息或警告消息以外的信息消息</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="time-stamp-field"></a>*time_stamp* field  
指示记录的事件发生时的系统时间。 *Time_stamp*字段是可选的 SetupAPI 默认不包括时间戳。 但是， [ **SetupWriteTextLog** ](https://msdn.microsoft.com/library/windows/hardware/ff552218)支持中的日志条目包括时间戳。 格式*time_stamp*字段是相同的格式*time_stamp*中所述的字段[文本日志部分标头的格式](format-of-a-text-log-section-header.md)。

<a href="" id="event-category-field"></a>*event_category* field  
表示所做的日志条目的安装程序 Api 操作的类别。 *Event_category*字段通常存在，但不是必需的。 如果*event_category*字段存在，它将包含下表中列出的字符串之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>Event_category</em>字段字符串</th>
<th align="left">安装程序 Api 操作</th>
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
<td align="left"><p>类安装程序或辅助安装程序操作</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"cpy: "</code></pre></td>
<td align="left"><p>将文件复制</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"dvi: "</code></pre></td>
<td align="left"><p>设备安装</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"flq: "</code></pre></td>
<td align="left"><p>管理文件的队列</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"inf: "</code></pre></td>
<td align="left"><p>管理 INF 文件</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"ndv: "</code></pre></td>
<td align="left"><p>新设备向导</p></td>
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
<td align="left"><p>管理驱动程序存储区</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"ui : "</code></pre></td>
<td align="left"><p>管理用户界面对话框</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"ump: "</code></pre></td>
<td align="left"><p>用户模式即插即用管理器</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="indentation-field"></a>*缩进*字段  
包含零个或多一系列*缩进单位*，其中的缩进单元是一个包含五个空格的 monospace 字符串。 *缩进*字段是可选的安装程序 Api 中不包括默认情况下的缩进。 **SetupWriteTextLog**支持更改的日志条目中包含的缩进单位数。

<a href="" id="formatted-message-field"></a>*formatted_message*字段  
包含适用于日志条目的特定信息。

记录的部分正文条目取决于为日志设置的事件级别和启用的日志类别级别。 有关这些设置的详细信息，请参阅[SetupAPI 日志记录注册表设置](setupapi-logging-registry-settings.md)。

当安装程序 Api 创建一个部分，其中将操作应用到设备安装，它还会以递归方式分组子节中的部分正文日志条目。 安装程序 Api 通过其批注和缩进日志条目的方式区分各小节。 在以下内容摘自一个典型的设备安装部分中将显示一个此类子节。 子部分开头的日志条目"dvi: {生成驱动程序列表}"结尾日志条目"dvi: {生成驱动程序列表-exit(0x00000000)}"。 此子部分显示中包含的日志条目的典型序列*entry_prefix*， *event_category*，*缩进*，和*formatted_message*字段。 编写了日志条目的安装程序 Api 操作还创建缩进，并提供格式化的消息的内容。 此示例中的事件级别已设置为 TXTLOG_DETAILS 并且已为此示例启用所有类别级别。

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

 

 





