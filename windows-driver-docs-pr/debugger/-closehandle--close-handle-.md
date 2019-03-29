---
title: .closehandle（关闭句柄）
description: .Closehandle 命令关闭目标应用程序拥有的句柄。
ms.assetid: 1513cbdd-327f-447a-8267-633cb123d17d
keywords:
- .closehandle （关闭句柄） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .closehandle (Close Handle)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 20ad6c9c453ad5ea1d28b090e3052fc7b1a7b63d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576447"
---
# <a name="closehandle-close-handle"></a>.closehandle（关闭句柄）


**.Closehandle**命令关闭目标应用程序拥有的句柄。

```dbgsyntax
.closehandle Handle 
.closehandle -a 
```

## <a name="span-idddkmetaclosehandledbgspanspan-idddkmetaclosehandledbgspanparameters"></a><span id="ddk_meta_close_handle_dbg"></span><span id="DDK_META_CLOSE_HANDLE_DBG"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
指定要关闭的句柄。

<span id="_______-a______"></span><span id="_______-A______"></span> **-a**   
导致要关闭目标应用程序拥有的所有句柄。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以使用[ **！ 处理**](-handle.md)扩展名，即可显示现有的句柄。

 

 





