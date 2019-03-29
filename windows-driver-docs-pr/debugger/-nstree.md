---
title: nstree
description: Nstree 扩展命名空间树中显示的 ACPI 命名空间对象与其子项。
ms.assetid: 0dec2a5a-ca77-4f91-9128-2d3dd8cd035f
keywords:
- nstree Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- nstree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a4b13fa75fec8c3efae4629c20843d76bf338bf5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576655"
---
# <a name="nstree"></a>!nstree


**！ Nstree**扩展命名空间树中显示的 ACPI 命名空间对象与其子项。

语法

```dbgcmd
!nstree [Address]
```

## <a name="span-idddknstreedbgspanspan-idddknstreedbgspanparameters"></a><span id="ddk__nstree_dbg"></span><span id="DDK__NSTREE_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的命名空间对象的地址。 将显示此对象和整个命名空间树从属于它。 如果*地址*是省略，将显示整个命名空间树。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[ACPI 调试](acpi-debugging.md)。

<a name="remarks"></a>备注
-------

此扩展等同于[ **！ amli dns /s**](-amli-dns.md)。

 

 





