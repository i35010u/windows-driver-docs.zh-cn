---
title: CTRL+R（重新同步）
description: CTRL + R 键同步到目标计算机。
keywords:
- CTRL + R (重新同步) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+R (Re-synchronize)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 13749f0da43126e07d0547fb6ab5820d973d03b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786985"
---
# <a name="ctrlr-re-synchronize"></a>CTRL+R（重新同步）


CTRL + R 键同步到目标计算机。

KD 语法

```dbgcmd
CTRL+R  ENTER 
```

WinDbg 语法

```dbgcmd
CTRL+ALT+R 
```

## <span id="ddk_meta_ctrl_r_dbg"></span><span id="DDK_META_CTRL_R_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>调试器</strong></p></td>
<td align="left"><p>仅限 KD 和 WinDbg</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关重新建立与目标的联系的其他方法，请参阅 [与目标计算机同步](synchronizing-with-the-target-computer.md)。

<a name="remarks"></a>备注
-------

这会尝试将主计算机与目标计算机同步。 如果目标未响应，请使用此密钥。

如果使用的是1394内核连接，则重新同步可能并不总是成功。

 

 





