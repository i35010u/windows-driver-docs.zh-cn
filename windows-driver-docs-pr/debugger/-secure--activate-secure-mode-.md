---
title: .secure（激活安全模式）
description: Secure 命令激活或显示安全模式的状态。
keywords:
- 。安全 (激活安全模式) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .secure (Activate Secure Mode)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b2d17ee181fd94709eff60da5cfd6c3a76e9750
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837563"
---
# <a name="secure-activate-secure-mode"></a>.secure（激活安全模式）


**Secure** 命令激活或显示安全模式的状态。

```dbgcmd
.secure 1 
.secure 
```

## <span id="ddk_meta_activate_secure_mode_dbg"></span><span id="DDK_META_ACTIVATE_SECURE_MODE_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

仅当调试器处于休眠状态时，才能启用安全模式。 安全模式仅适用于内核模式会话，因为根据定义，安全模式会阻止用户模式的调试操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [安全模式](secure-mode.md)。

<a name="remarks"></a>备注
-------

若要激活安全模式，请使用命令 **。 secure 1** (或 **. secure** 后跟) 的任何非零值。

命令 **。 secure** 将显示安全模式当前是否处于活动状态。

 

 





