---
title: amli bl
description: Amli bl 扩展显示所有 AML 断点的列表。
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
ms.openlocfilehash: a38fdc630e709d81d05af6c27d669a7baba209e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800109"
---
# <a name="amli-bl"></a>!amli bl


**！ Amli bl** 扩展显示所有 AML 断点的列表。

语法

```dbgcmd
   !amli bl
```

## <span id="ddk__amli_bl_dbg"></span><span id="DDK__AMLI_BL_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅 [AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

AMLI 调试器最多支持10个断点。

下面是 **！ amli bl** 扩展的一个示例：

```console
kd> !amli bl
 0: <e> ffffffff80e5e2f1:[\_SB.LNKD._SRS]
 1: <e> ffffffff80e5d969:[\_SB.LNKB._STA]
 2: <d> ffffffff80e630c9:[\_WAK]
 3: <e> ffffffff80e612c9:[\_SB.MBRD._CRS]
```

第一列提供断点号。 **&lt; E &gt;** 和 **&lt; d &gt;** 标记指示是启用还是禁用断点。 断点的地址在下一列中。 最后，将列出包含该断点的方法，并在该方法启动时未设置断点偏移量。

 

 





