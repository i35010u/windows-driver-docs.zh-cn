---
title: amli bl
description: Amli bl 扩展显示所有 AML 断点的列表。
ms.assetid: 4ce52006-d44e-40ab-b669-2aa9509b6b21
keywords:
- amli bl Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli bl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aeb69d43659916b55b6b9239733b167ba9e2f363
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519702"
---
# <a name="amli-bl"></a>！ amli bl


**！ Amli bl**扩展插件都会显示所有 AML 断点的列表。

语法

```dbgcmd
   !amli bl
```

## <span id="ddk__amli_bl_dbg"></span><span id="DDK__AMLI_BL_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

AMLI 调试器支持最多十个断点。

下面是举例 **！ amli bl**扩展：

```console
kd> !amli bl
 0: <e> ffffffff80e5e2f1:[\_SB.LNKD._SRS]
 1: <e> ffffffff80e5d969:[\_SB.LNKB._STA]
 2: <d> ffffffff80e630c9:[\_WAK]
 3: <e> ffffffff80e612c9:[\_SB.MBRD._CRS]
```

第一列给出断点数。 **&lt;E&gt;** 并**&lt;d&gt;** 标记指示是否启用或禁用断点。 在下一列中的断点的地址。 最后，包含该断点的方法被列出，如果该方法开始时未设置的断点的偏移量。

 

 





