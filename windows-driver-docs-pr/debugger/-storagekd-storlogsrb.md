---
title: storagekd.storlogsrb
description: Storagekd.storlogsrb 扩展显示为筛选的存储 （或 SCSI） 适配器 Storport 的内部日志项请求块 (SRB) 提供。
ms.assetid: 9E742636-DD19-4D8D-BDA1-C9BB8C293D8C
keywords:
- storagekd.storlogsrb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storlogsrb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ce1d0a0624552e02bc9231615a02d4925848b8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520109"
---
# <a name="storagekdstorlogsrb"></a>!storagekd.storlogsrb


**！ Storagekd.storlogsrb**扩展显示为筛选的存储 （或 SCSI） 适配器 Storport 的内部日志项请求块 (SRB) 提供。

```dbgcmd
!storagekd.storlogsrb <Address> <srb> [<starting_entry> [<ending_entry>]] [L <count>]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定 Storport 适配器设备扩展或设备对象的地址。

<span id="_______SRB______"></span><span id="_______srb______"></span> *SRB*   
若要找到 SRB。

<span id="_______starting_entry______"></span><span id="_______STARTING_ENTRY______"></span> *启动\_条目*   
要显示的区域中的开始条目中。 如果未指定，上次*计数*不会显示条目。

<span id="_______ending_entry______"></span><span id="_______ENDING_ENTRY______"></span> *ending\_entry*   
中要显示的范围的结束条目。 如果未指定，*计数*将显示条目，从指定的项目开始*启动\_条目*。

<span id="_______count______"></span><span id="_______COUNT______"></span> *count*   
若要显示的项计数。 如果未指定，使用值为 50。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 及更高版本</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

 

 





