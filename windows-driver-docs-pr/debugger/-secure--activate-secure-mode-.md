---
title: .secure（激活安全模式）
description: 激活的.secure 命令或显示的安全模式下的状态。
ms.assetid: 58a8936e-898f-4608-b1b0-399d5152f410
keywords:
- .secure （激活安全模式下） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .secure (Activate Secure Mode)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c22b9876bc2f237acf5faee7364301b2e6c278f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339810"
---
# <a name="secure-activate-secure-mode"></a>.secure（激活安全模式）


**.Secure**命令激活或显示的安全模式下的状态。

```dbgcmd
.secure 1 
.secure 
```

## <span id="ddk_meta_activate_secure_mode_dbg"></span><span id="DDK_META_ACTIVATE_SECURE_MODE_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

在调试器处于休眠状态时，可以只启用安全模式。 安全模式下仅适用于内核模式会话中因为根据定义，安全模式可以防止用户模式下调试操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[安全模式下](secure-mode.md)。

<a name="remarks"></a>备注
-------

若要激活安全模式下，使用命令 **.secure 1** (或 **.secure**跟任何非零值)。

该命令 **.secure**将显示安全模式下是否为当前处于活动状态。

 

 





