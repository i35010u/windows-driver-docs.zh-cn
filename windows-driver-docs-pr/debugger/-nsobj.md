---
title: nsobj
description: Nsobj 扩展显示 ACPI 命名空间对象。
ms.assetid: 348aeb42-41c6-42de-bb43-b075f55076c4
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
ms.openlocfilehash: 6fa7464ca3cd5439aad8367189283e02f8f27d4d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544281"
---
# <a name="nsobj"></a>!nsobj


**！ Nsobj**扩展显示 ACPI 命名空间对象。

语法

```dbgcmd
!nsobj [Address]
```

## <a name="span-idddknsobjdbgspanspan-idddknsobjdbgspanparameters"></a><span id="ddk__nsobj_dbg"></span><span id="DDK__NSOBJ_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的命名空间对象的地址。 如果省略此属性，则使用命名空间树的根。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[ACPI 调试](acpi-debugging.md)。

<a name="remarks"></a>备注
-------

此扩展等同于[ **！ amli dns**](-amli-dns.md)。

 

 





