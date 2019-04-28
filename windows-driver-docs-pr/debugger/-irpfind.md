---
title: irpfind
description: Irpfind 扩展显示当前分配的在目标系统中，或指定的搜索条件匹配的那些 Irp 有关所有 I/O 请求数据包 (IRP) 有关的信息。
ms.assetid: f0d850d9-8804-40df-90a3-b9c6a6b4540f
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
ms.openlocfilehash: fede13a247b35ebc4ec556b41a461c1eac7354d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336390"
---
# <a name="irpfind"></a>!irpfind


**！ Irpfind**扩展显示有关所有 I/O 请求数据包 (IRP) 当前分配的目标系统中，或指定的搜索条件匹配的那些 Irp 的信息。

语法

```dbgcmd
!irpfind [-v][PoolType[RestartAddress[CriteriaData]]]
```

## <a name="span-idddkirpfinddbgspanspan-idddkirpfinddbgspanparameters"></a><span id="ddk__irpfind_dbg"></span><span id="DDK__IRPFIND_DBG"></span>参数


<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
显示详细的信息。

<span id="_______PoolType______"></span><span id="_______pooltype______"></span><span id="_______POOLTYPE______"></span> *PoolType*   
指定要搜索的池的类型。 允许使用以下值：

<span id="0"></span>0  
指定非分页的内存池。 这是默认设置。

<span id="1"></span>1  
指定分页的内存池。

<span id="2"></span>2  
指定特殊的池。

<span id="4"></span>4  
指定的会话池。

<span id="_______RestartAddress______"></span><span id="_______restartaddress______"></span><span id="_______RESTARTADDRESS______"></span> *RestartAddress*   
指定要开始搜索的十六进制地址。 这是上一次搜索已过早终止的情况下很有用。 默认值为 0。

<span id="_______Criteria______"></span><span id="_______criteria______"></span><span id="_______CRITERIA______"></span> *条件*   
指定用于搜索的条件。 仅这些 Irp 满足给定的匹配项将会显示。

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
<td align="left"><p><strong>arg</strong></p></td>
<td align="left"><p>查找与其中一个参数等于的堆栈位置的所有 Irp<em>数据</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>device</strong></p></td>
<td align="left"><p>查找所有 Irp 堆栈位置使用其中<strong>DeviceObject</strong>等于<em>数据</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>fileobject</strong></p></td>
<td align="left"><p>查找所有 Irp 其<strong>Irp.Tail.Overlay.OriginalFileObject</strong>等于<em>数据</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>mdlprocess</strong></p></td>
<td align="left"><p>查找所有 Irp 其<strong>Irp.MdlAddress.Process</strong>等于<em>数据</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>thread</strong></p></td>
<td align="left"><p>查找所有 Irp 其<strong>Irp.Tail.Overlay.Thread</strong>等于<em>数据</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>userevent</strong></p></td>
<td align="left"><p>查找所有 Irp 其<strong>Irp.UserEvent</strong>等于<em>数据</em>。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Data______"></span><span id="_______data______"></span><span id="_______DATA______"></span> *数据*   
指定在搜索匹配的数据。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

请参阅[插调试](plug-and-play-debugging.md)对于此扩展命令的应用程序。 有关 Irp 的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。

<a name="remarks"></a>备注
-------

此示例中的非分页池的设置完成后的用户事件 FF9E4F48 查找 IRP:

```dbgcmd
kd> !irpfind 0 0 userevent ff9e4f48
```

下面的示例生成非分页缓冲池中的所有 Irp 的完整列表：

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

 

 





