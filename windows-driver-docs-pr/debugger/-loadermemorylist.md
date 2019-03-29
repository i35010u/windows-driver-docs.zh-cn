---
title: loadermemorylist
description: Loadermemorylist 扩展显示 Windows 到 Windows 启动加载程序传递的内存分配列表。
ms.assetid: 3e5dff7a-ea8f-4029-93e3-7c160487e968
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
ms.openlocfilehash: 7fd3db55d67c45bfe3b7874407f0a9706c3c44ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563512"
---
# <a name="loadermemorylist"></a>!loadermemorylist


**！ Loadermemorylist**扩展显示 Windows 到 Windows 启动加载程序传递的内存分配列表。

```dbgcmd
!loadermemorylist ListHeadAddress
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______ListHeadAddress______"></span><span id="_______listheadaddress______"></span><span id="_______LISTHEADADDRESS______"></span> *ListHeadAddress*   
指定列表标头的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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
<td align="left"><p><strong>Windows Vista 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此扩展旨在 Ntldr 运行时在系统启动过程的开头使用。 它显示包含开始时间、 结束时和类型的每个页面范围的内存分配列表。

可以通过按 CTRL + BREAK （在 WinDbg) 或 CTRL + C （中 KD) 来停止执行任何时候。

 

 





