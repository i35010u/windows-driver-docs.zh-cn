---
title: .noversion（禁用版本检查）
description: Noversion 命令禁用对扩展 Dll 的所有版本检查。
keywords:
- " ( 中禁用版本检查) 命令"
- 。 noversion (禁用版本检查) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .noversion (Disable Version Checking)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cd0b84c88cd276ae7669ad430ba33f9f31cdc046
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803305"
---
# <a name="noversion-disable-version-checking"></a>.noversion（禁用版本检查）


**Noversion** 命令禁用对扩展 dll 的所有版本检查。

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
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

扩展 Dll 的内部版本号应与您正在调试的计算机的生成号匹配，因为 Dll 是用依赖于特定版本的数据结构的依赖项编译和链接的。 如果版本不匹配，通常会收到以下消息。

```console
*** Extension DLL(1367 Free) does not match target system(1552 Free) 
```

 

 





