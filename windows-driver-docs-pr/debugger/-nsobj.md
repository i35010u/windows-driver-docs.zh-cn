---
title: nsobj
description: Nsobj 扩展显示 ACPI 命名空间对象。
keywords:
- nsobj Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- nsobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2de9d87913adaad9a2679f3cefa56bbba5d84c11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803301"
---
# <a name="nsobj"></a>!nsobj


**！ Nsobj** 扩展显示 ACPI 命名空间对象。

语法

```dbgcmd
!nsobj [Address]
```

## <a name="span-idddk__nsobj_dbgspanspan-idddk__nsobj_dbgspanparameters"></a><span id="ddk__nsobj_dbg"></span><span id="DDK__NSOBJ_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定命名空间对象的地址。 如果省略此，则使用命名空间树的根。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [ACPI 调试](acpi-debugging.md)。

<a name="remarks"></a>备注
-------

此扩展等效于 [**！ amli dns**](-amli-dns.md)。

 

 





