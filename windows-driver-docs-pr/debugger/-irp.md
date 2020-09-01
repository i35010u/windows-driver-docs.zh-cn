---
title: irp 扩展命令
description: Irp 扩展显示有关 i/o 请求数据包 (IRP) 的信息。
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
ms.openlocfilehash: 156fee361c9033ecef5b39c06796dcd0e15c4e2b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217102"
---
# <a name="irp"></a>!irp


**！ Irp**扩展显示有关 i/o 请求数据包 (irp) 的信息。

```dbgcmd
!irp Address [Detail] 
```

## <a name="span-idddk__irp_dbgspanspan-idddk__irp_dbgspanparameters"></a><span id="ddk__irp_dbg"></span><span id="DDK__IRP_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 IRP 的十六进制地址。

<span id="_______Detail______"></span><span id="_______detail______"></span><span id="_______DETAIL______"></span>*详细信息*   
如果此参数包含在任何值中（例如1），则输出将包括 IRP 的状态、其内存描述符列表的地址 (MDL) 、其拥有的线程和其所有 i/o 堆栈的堆栈信息，以及 IRP 的每个堆栈位置的相关信息，其中包括主要函数代码和次要函数代码的十六进制版本。 如果省略此参数，则输出将只包含信息的摘要。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

请参阅 [即插即用调试](plug-and-play-debugging.md) 和调试此扩展命令应用程序的 [中断风暴](debugging-an-interrupt-storm.md) 。 有关 Irp 的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，Mark Russinovich 和 David 所罗门群岛。 有关主要和次要函数代码的详细信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

本主题介绍 IRP 结构 [**irp**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)。

有关对 IRP 结构（包括返回的参数）进行解码的详细信息，请参阅以下资源。

- Windows 内部机制，Russinovich，David 为所罗门群岛和 Alex Ionescu
- 开发包含 Windows Driver Foundation 人员 Smith 和 Orwick 的驱动程序


<a name="remarks"></a>备注
-------

输出还指示在完成 IRP 并处理堆栈位置之后，每个堆栈位置的完成例程将在什么条件下调用。 有三种可能性：

<span id="________Success"></span><span id="________success"></span><span id="________SUCCESS"></span>**成功**  
指示当 IRP 完成后，将调用完成例程并显示成功代码。

<span id="________Error"></span><span id="________error"></span><span id="________ERROR"></span>**错误**  
指示在完成 IRP 后，将调用完成例程，并显示错误代码。

<span id="________Cancel"></span><span id="________cancel"></span><span id="________CANCEL"></span>**取消**  
指示如果尝试取消 IRP，将调用完成例程。

这三种情况的任意组合都可能出现，并且如果满足显示的任何条件，则将调用完成例程。 适当的值列在有关每个堆栈位置的信息的第一行的末尾，紧跟在 **完成上下文** 项之后。

下面是适用于 Windows 10 的此扩展的输出示例：

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

从 Windows 10 开始，将显示 IRP 的主要和次要代码文本，例如，"IRP \_ MJ \_ 文件 \_ 系统 \_ 控制" 此代码值还以十六进制显示，在本例中为 " (d) "。

输出中显示的第三个参数是 IOCTL 代码。 使用 [**！ ioctldecode**](-ioctldecode.md) 命令显示有关 IOCTL 的信息。

下面是来自 Windows Vista 的此扩展的输出示例。

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

请注意，驱动程序名称旁边的完成例程是在该堆栈位置上设置的，它是由驱动程序在下面的行中设置的。 在前面的示例中， **ntfs！ NtfsMasterIrpSyncCompletionRoutine**由** \\ FileSystem \\ ntfs**设置。 **Ntfs！ NtfsMasterIrpSyncCompletionRoutine**， **847eeed0-829E2ba8**以上的**完成上下文**项指示完成例程的地址以及将传递到**Ntfs！ NtfsMasterIrpSyncCompletionRoutine**的上下文。 从这里可以看到， **Ntfs！ NtfsMasterIrpSyncCompletionRoutine** 的地址为 **847eeed0**，并且在调用时将传递给此例程的上下文为 **829e2ba8**。

**IRP 主要功能代码**

包括下列信息以帮助你解释此扩展命令的输出。

IRP 主要功能代码如下：

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

 

即插即用次要函数代码如下所示：

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

 

电源管理次要功能代码如下：

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

 

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**!irpfind**](-irpfind.md)

[**!ioctldecode**](-ioctldecode.md)

 

