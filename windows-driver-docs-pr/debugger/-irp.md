---
title: irp 扩展命令
description: Irp 扩展显示 I/O 请求数据包 (IRP) 有关的信息。
ms.assetid: 2260255d-813b-4b89-8dbe-6ce7e5596ccf
keywords:
- IRP
- IRP
- IO 请求数据包
- irp Windows 调试
ms.date: 08/23/2018
topic_type:
- apiref
api_name:
- irp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 17b1e03b9936675fb38758ddc4a1d26fe622c762
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567385"
---
# <a name="irp"></a>!irp


**！ Irp**扩展显示 I/O 请求数据包 (IRP) 有关的信息。

```dbgcmd
!irp Address [Detail] 
```

## <a name="span-idddkirpdbgspanspan-idddkirpdbgspanparameters"></a><span id="ddk__irp_dbg"></span><span id="DDK__IRP_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的 IRP 十六进制的地址。

<span id="_______Detail______"></span><span id="_______detail______"></span><span id="_______DETAIL______"></span> *详细信息*   
如果此参数为包含任何值，如 1，输出包括 IRP 的状态、 其内存描述符列表 (MDL)，其拥有线程和所有其 I/O 堆栈的堆栈信息和 IRP 的每个堆栈位置有关的信息的地址包括主要函数代码和次函数代码的十六进制版本。 如果省略此参数，输出中包括的信息的摘要。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

请参阅[插调试](plug-and-play-debugging.md)并[调试中断风暴](debugging-an-interrupt-storm.md)对于此扩展命令的应用程序。 有关 Irp 的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 主要和次要函数代码的详细信息，请参阅 Windows Driver Kit (WDK) 文档。 （这些资源可能不可用在某些语言和国家/地区中。）

本主题介绍 IRP 结构[ **IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)。

解码 IRP 结构包括返回的参数的详细信息，请参阅以下资源。

- Mark E.Russinovich、 David A.Solomon 和 Alex Ionescu Windows 内部结构
- 使用 Windows Driver Foundation 专家 Smith 和尾 Orwick 开发驱动程序


<a name="remarks"></a>备注
-------

输出还指示一旦 IRP 已经完成并经过处理的堆栈位置，则将调用在什么条件下每个堆栈位置完成例程。 有三种可能性：

<span id="________Success"></span><span id="________success"></span><span id="________SUCCESS"></span> **成功**  
指示当 IRP 已完成，但成功代码时，将调用完成例程。

<span id="________Error"></span><span id="________error"></span><span id="________ERROR"></span> **错误**  
指示 IRP 完成并返回错误代码时，将调用完成例程。

<span id="________Cancel"></span><span id="________cancel"></span><span id="________CANCEL"></span> **Cancel**  
指示是否尝试取消 IRP，将调用完成例程。

这三个字段的任意组合可能会出现，并且如果满足任何条件所示，将调用完成例程。 适当的值每个堆栈位置有关的信息的第一行的结尾处列出后立即**完成上下文**条目。

下面是输出的此扩展适用于 Windows 10 示例：

```dbgcmd
0: kd> !irp ac598dc8
Irp is active with 2 stacks 1 is current (= 0xac598e38)
 No Mdl: No System Buffer: Thread 8d1c7bc0:  Irp stack trace.  
     cmd  flg cl Device   File     Completion-Context
>[IRP_MJ_FILE_SYSTEM_CONTROL(d), N/A(0)]
            1 e1 8a6434d8 ac598d40 853220cb-a89682d8 Success Error Cancel pending
           \FileSystem\Npfs fltmgr!FltpPassThroughCompletion
            Args: 00000000 00000000 00110008 00000000
 [IRP_MJ_FILE_SYSTEM_CONTROL(d), N/A(0)]
            1  0 8a799710 ac598d40 00000000-00000000    
           \FileSystem\FltMgr
            Args: 00000000 00000000 0x00110008 00000000
```

从 Windows 10 开始 IRP 主版本号和次代码文本显示，例如，"IRP\_MJ\_文件\_系统\_控件"的代码值也显示在十六进制，在此示例中"(d)"。

显示在输出中，第三个参数是 IOCTL 代码。 使用[ **！ ioctldecode** ](-ioctldecode.md)命令以显示有关 IOCTL 的信息。

下面是输出的从 Windows Vista 中此扩展示例。

```dbgcmd
0: kd> !irp 0x831f4a00
Irp is active with 8 stacks 5 is current (= 0x831f4b00)
 Mdl = 82b020d8 Thread 8c622118:  Irp stack trace.
     cmd  flg cl Device   File     Completion-Context
 [  0, 0]   0  0 00000000 00000000 00000000-00000000

                        Args: 00000000 00000000 00000000 00000000
 [  0, 0]   0  0 00000000 00000000 00000000-00000000

                        Args: 00000000 00000000 00000000 00000000
 [  0, 0]   0  0 00000000 00000000 00000000-00000000

                        Args: 00000000 00000000 00000000 00000000
 [  0, 0]   0  0 00000000 00000000 00000000-00000000

                        Args: 00000000 00000000 00000000 00000000
>[  3,34]  40 e1 828517a8 00000000 842511e0-00000000 Success Error Cancel pending
               \Driver\disk     partmgr!PmReadWriteCompletion
 Args: 00007000 00000000 fe084e00 00000004
 [  3, 0]  40 e0 82851450 00000000 842414d4-82956350 Success Error Cancel
 \Driver\PartMgr  volmgr!VmpReadWriteCompletionRoutine
                        Args: 129131bb 000000de fe084e00 00000004
 [  3, 0]   0 e0 82956298 00000000 847eeed0-829e2ba8 Success Error Cancel
 \Driver\volmgr   Ntfs!NtfsMasterIrpSyncCompletionRoutine
                        Args: 00007000 00000000 1bdae400 00000000
 [  3, 0]   0  0 82ac2020 8e879410 00000000-00000000
               \FileSystem\Ntfs
                        Args: 00007000 00000000 00018400 00000000
```

请注意，驱动程序名称旁边的完成例程设置上该堆栈的位置，它由下面的行中的驱动程序设置。 在前面的示例中， **Ntfs ！ NtfsMasterIrpSyncCompletionRoutine**由设置**\\文件系统\\Ntfs**。 **完成上下文**上文条目**Ntfs ！ NtfsMasterIrpSyncCompletionRoutine**， **847eeed0 829e2ba8**，指示完成例程的地址作为上下文将传递给**Ntfs ！ NtfsMasterIrpSyncCompletionRoutine**。 从此我们可以看到的地址**Ntfs ！ NtfsMasterIrpSyncCompletionRoutine**是**847eeed0**，且被调用时将传递给此例程的上下文是**829e2ba8**.

**IRP 主要函数代码**

若要帮助您解释此扩展命令的输出中包含以下信息。

IRP 主要函数代码如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主要函数代码</th>
<th align="left">十六进制代码</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MJ_CREATE</p></td>
<td align="left"><p>0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_CREATE_NAMED_PIPE</p></td>
<td align="left"><p>0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_CLOSE</p></td>
<td align="left"><p>0x02</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_READ</p></td>
<td align="left"><p>0x03</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_WRITE</p></td>
<td align="left"><p>0x04</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_QUERY_INFORMATION</p></td>
<td align="left"><p>0x05</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_SET_INFORMATION</p></td>
<td align="left"><p>0x06</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_QUERY_EA</p></td>
<td align="left"><p>0x07</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_SET_EA</p></td>
<td align="left"><p>0x08</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_FLUSH_BUFFERS</p></td>
<td align="left"><p>0x09</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_QUERY_VOLUME_INFORMATION</p></td>
<td align="left"><p>0x0A</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_SET_VOLUME_INFORMATION</p></td>
<td align="left"><p>0x0B</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_DIRECTORY_CONTROL</p></td>
<td align="left"><p>0x0C</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_FILE_SYSTEM_CONTROL</p></td>
<td align="left"><p>0x0D</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_DEVICE_CONTROL</p></td>
<td align="left"><p>0x0E</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
IRP_MJ_INTERNAL_DEVICE_CONTROL IRP_MJ_SCSI</td>
<td align="left"><p>0x0F</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_SHUTDOWN</p></td>
<td align="left"><p>0x10</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_LOCK_CONTROL</p></td>
<td align="left"><p>0x11</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_CLEANUP</p></td>
<td align="left"><p>0x12</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_CREATE_MAILSLOT</p></td>
<td align="left"><p>0x13</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_QUERY_SECURITY</p></td>
<td align="left"><p>0x14</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_SET_SECURITY</p></td>
<td align="left"><p>0x15</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_POWER</p></td>
<td align="left"><p>0x16</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_SYSTEM_CONTROL</p></td>
<td align="left"><p>0x17</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_DEVICE_CHANGE</p></td>
<td align="left"><p>0x18</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_QUERY_QUOTA</p></td>
<td align="left"><p>0x19</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_SET_QUOTA</p></td>
<td align="left"><p>0x1A</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
IRP_MJ_PNP IRP_MJ_MAXIMUM_FUNCTION</td>
<td align="left"><p>0x1B</p></td>
</tr>
</tbody>
</table>

 

插次要函数代码如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">次要函数代码</th>
<th align="left">十六进制代码</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_START_DEVICE</p></td>
<td align="left"><p>0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_REMOVE_DEVICE</p></td>
<td align="left"><p>0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_REMOVE_DEVICE</p></td>
<td align="left"><p>0x02</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_CANCEL_REMOVE_DEVICE</p></td>
<td align="left"><p>0x03</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_STOP_DEVICE</p></td>
<td align="left"><p>0x04</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_STOP_DEVICE</p></td>
<td align="left"><p>0x05</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_CANCEL_STOP_DEVICE</p></td>
<td align="left"><p>0x06</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_DEVICE_RELATIONS</p></td>
<td align="left"><p>0x07</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_QUERY_INTERFACE</p></td>
<td align="left"><p>0x08</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_CAPABILITIES</p></td>
<td align="left"><p>0x09</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_QUERY_RESOURCES</p></td>
<td align="left"><p>0x0A</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_RESOURCE_REQUIREMENTS</p></td>
<td align="left"><p>0x0B</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_QUERY_DEVICE_TEXT</p></td>
<td align="left"><p>0x0C</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_FILTER_RESOURCE_REQUIREMENTS</p></td>
<td align="left"><p>0x0D</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_READ_CONFIG</p></td>
<td align="left"><p>0x0F</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_WRITE_CONFIG</p></td>
<td align="left"><p>0x10</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_EJECT</p></td>
<td align="left"><p>0x11</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_SET_LOCK</p></td>
<td align="left"><p>0x12</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_QUERY_ID</p></td>
<td align="left"><p>0x13</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_PNP_DEVICE_STATE</p></td>
<td align="left"><p>0x14</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_QUERY_BUS_INFORMATION</p></td>
<td align="left"><p>0x15</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_DEVICE_USAGE_NOTIFICATION</p></td>
<td align="left"><p>0x16</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_SURPRISE_REMOVAL</p></td>
<td align="left"><p>0x17</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_LEGACY_BUS_INFORMATION</p></td>
<td align="left"><p>0x18</p></td>
</tr>
</tbody>
</table>

 

WMI 次要函数代码如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">次要函数代码</th>
<th align="left">十六进制代码</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_QUERY_ALL_DATA</p></td>
<td align="left"><p>0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_SINGLE_INSTANCE</p></td>
<td align="left"><p>0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_CHANGE_SINGLE_INSTANCE</p></td>
<td align="left"><p>0x02</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_CHANGE_SINGLE_ITEM</p></td>
<td align="left"><p>0x03</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_ENABLE_EVENTS</p></td>
<td align="left"><p>0x04</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_DISABLE_EVENTS</p></td>
<td align="left"><p>0x05</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_ENABLE_COLLECTION</p></td>
<td align="left"><p>0x06</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_DISABLE_COLLECTION</p></td>
<td align="left"><p>0x07</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_REGINFO</p></td>
<td align="left"><p>0x08</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_EXECUTE_METHOD</p></td>
<td align="left"><p>0x09</p></td>
</tr>
</tbody>
</table>

 

电源管理次要函数代码如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">次要函数代码</th>
<th align="left">十六进制代码</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_WAIT_WAKE</p></td>
<td align="left"><p>0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_POWER_SEQUENCE</p></td>
<td align="left"><p>0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_SET_POWER</p></td>
<td align="left"><p>0x02</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_POWER</p></td>
<td align="left"><p>0x03</p></td>
</tr>
</tbody>
</table>

 

SCSI 次要函数代码如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">次要函数代码</th>
<th align="left">十六进制代码</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_SCSI_CLASS</p></td>
<td align="left"><p>0x01</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**!irpfind**](-irpfind.md)

[**!ioctldecode**](-ioctldecode.md)

 

 






