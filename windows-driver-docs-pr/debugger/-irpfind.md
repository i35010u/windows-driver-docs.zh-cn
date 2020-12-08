---
title: irpfind
description: Irpfind 扩展显示当前在目标系统中分配 (IRP) 的所有 i/o 请求包的相关信息，以及与指定的搜索条件匹配的那些 Irp。
keywords:
- irpfind Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- irpfind
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: db382518237cf0f17d8e37821cd6b77e5c2199c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798445"
---
# <a name="irpfind"></a>!irpfind


**！ Irpfind** extension 显示有关当前在目标系统中分配的所有 i/o 请求数据包 (IRP) 的信息，或者与与指定的搜索条件匹配的那些 irp 有关的信息。

语法

```dbgcmd
!irpfind [-v][PoolType[RestartAddress[CriteriaData]]]
```

## <a name="span-idddk__irpfind_dbgspanspan-idddk__irpfind_dbgspanparameters"></a><span id="ddk__irpfind_dbg"></span><span id="DDK__IRPFIND_DBG"></span>参数


<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
显示详细信息。

<span id="_______PoolType______"></span><span id="_______pooltype______"></span><span id="_______POOLTYPE______"></span>*PoolType*   
指定要搜索的池的类型。 允许使用以下值：

<span id="0"></span>0  
指定非分页内存池。 这是默认值。

<span id="1"></span>1  
指定分页内存池。

<span id="2"></span>2  
指定特殊池。

<span id="4"></span>4  
指定会话池。

<span id="_______RestartAddress______"></span><span id="_______restartaddress______"></span><span id="_______RESTARTADDRESS______"></span>*RestartAddress*   
指定从其开始搜索的十六进制地址。 如果以前的搜索提前终止，这会很有用。 默认值为零。

<span id="_______Criteria______"></span><span id="_______criteria______"></span><span id="_______CRITERIA______"></span>*条件*   
指定搜索条件。 将仅显示那些满足给定匹配项的 Irp。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">条件</th>
<th align="left">匹配</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>与我们联系</strong></p></td>
<td align="left"><p>查找所有具有堆栈位置的 Irp，其中其中一个参数等于 <em>Data</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>设备</strong></p></td>
<td align="left"><p>查找堆栈位置的所有 Irp，其中 <strong>DeviceObject</strong> 等于 <em>Data</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>fileobject</strong></p></td>
<td align="left"><p>查找其 <strong>Irp OriginalFileObject</strong> 等于 <em>Data</em>的所有 irp。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>mdlprocess</strong></p></td>
<td align="left"><p>查找其 <strong>MdlAddress</strong> 等于 <em>Data</em>的所有 irp。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>thread</strong></p></td>
<td align="left"><p>查找其 <strong>Irp</strong> 为 " <em>数据</em>" 的所有 irp。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>userevent</strong></p></td>
<td align="left"><p>查找其 <strong>UserEvent</strong> 等于 <em>Data</em>的所有 irp。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Data______"></span><span id="_______data______"></span><span id="_______DATA______"></span>*数据*   
指定要在搜索中匹配的数据。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

请参阅 [即插即用调试](plug-and-play-debugging.md) 此扩展命令的应用程序。 有关 Irp 的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，Mark Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

此示例在非分页池中查找要在完成时设置用户事件 FF9E4F48 的 IRP：

```dbgcmd
kd> !irpfind 0 0 userevent ff9e4f48
```

下面的示例生成非分页池中所有 Irp 的完整列表：

```dbgcmd
kd> !irpfind
Searching NonPaged pool (8090c000 : 8131e000) for Tag: Irp
8097c008 Thread 8094d900 current stack belongs to  \Driver\symc810
8097dec8 Thread 8094dda0 current stack belongs to  \FileSystem\Ntfs
809861a8 Thread 8094dda0 current stack belongs to  \Driver\symc810
809864e8 Thread 80951ba0 current stack belongs to  \Driver\Mouclass
80986608 Thread 80951ba0 current stack belongs to  \Driver\Kbdclass
80986728 Thread 8094dda0 current stack belongs to  \Driver\symc810
```

 

 





