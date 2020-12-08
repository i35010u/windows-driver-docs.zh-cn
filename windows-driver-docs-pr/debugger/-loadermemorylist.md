---
title: loadermemorylist
description: Loadermemorylist 扩展显示 Windows 启动加载程序传递到 Windows 的内存分配列表。
keywords:
- OSLOADER
- loadermemorylist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- loadermemorylist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 287fa2f2c7c40b339ca6b46583ab0ea1640a6e80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814667"
---
# <a name="loadermemorylist"></a>!loadermemorylist


**！ Loadermemorylist** Extension 显示 windows 启动加载程序传递到 windows 的内存分配列表。

```dbgcmd
!loadermemorylist ListHeadAddress
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______ListHeadAddress______"></span><span id="_______listheadaddress______"></span><span id="_______LISTHEADADDRESS______"></span>*ListHeadAddress*   
指定列表标头的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP</strong></p>
<p><strong>Windows Server 2003</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Vista 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此扩展旨在在 Ntldr 运行时在系统启动过程开始时使用。 它显示一个内存分配列表，其中包含每个页面范围的开始、结束和类型。

您可以通过在 WinDbg) 中按 CTRL + BREAK (或在 KD) 中按 CTRL + C (，随时停止执行。

 

 





