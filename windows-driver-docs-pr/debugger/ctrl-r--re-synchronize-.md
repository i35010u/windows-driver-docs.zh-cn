---
title: CTRL + R （重新同步）
description: CTRL + R 键将与目标计算机同步。
ms.assetid: 95ffa380-af90-4d56-b973-038e7ccc6760
keywords:
- CTRL + R （重新同步） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+R (Re-synchronize)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fb95a8994c80d6cc36432ae71eb9ac064bb33229
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547160"
---
# <a name="ctrlr-re-synchronize"></a>CTRL + R （重新同步）


CTRL + R 键将与目标计算机同步。

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
<td align="left"><p>KD 和 WinDbg 仅</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关重新建立与目标的联系的其他方法，请参阅[与目标计算机同步](synchronizing-with-the-target-computer.md)。

<a name="remarks"></a>备注
-------

此操作只能与目标计算机同步主机计算机。 如果目标没有响应，请使用此密钥。

如果使用的 1394年内核连接，重新同步可能始终会失败。

 

 





