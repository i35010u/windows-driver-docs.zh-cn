---
title: .noversion（禁用版本检查）
description: .Noversion 命令禁用所有版本检查的扩展 Dll。
ms.assetid: ce7fbff4-7936-4bef-8236-a13957ada7f4
keywords:
- 禁用版本检查 (.noversion) 命令
- .noversion （禁用版本检查） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .noversion (Disable Version Checking)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a1c329dba7aa9953fb4210fd32996dd42bc62146
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335864"
---
# <a name="noversion-disable-version-checking"></a>.noversion（禁用版本检查）


**.Noversion**命令禁用所有版本检查的扩展 Dll。

```dbgcmd
.noversion
```

## <span id="ddk_meta_disable_version_checking_dbg"></span><span id="DDK_META_DISABLE_VERSION_CHECKING_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

扩展 Dll 的生成号应与你正在调试，因为这些 Dll 是编译，与特定版本的数据结构上的依赖关系链接的计算机的生成号匹配。 如果版本不匹配，您通常收到以下消息。

```console
*** Extension DLL(1367 Free) does not match target system(1552 Free) 
```

 

 





