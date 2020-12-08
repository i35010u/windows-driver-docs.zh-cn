---
title: nstree
description: Nstree 扩展在命名空间树中显示 ACPI 命名空间对象及其子级。
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
ms.openlocfilehash: 50ef477e690ffa14b744d1a7f8fcbd1b2d64f547
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803299"
---
# <a name="nstree"></a>!nstree


**！ Nstree** extension 在命名空间树中显示 ACPI 命名空间对象及其子级。

语法

```dbgcmd
!nstree [Address]
```

## <a name="span-idddk__nstree_dbgspanspan-idddk__nstree_dbgspanparameters"></a><span id="ddk__nstree_dbg"></span><span id="DDK__NSTREE_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定命名空间对象的地址。 此时将显示此对象和从属于该对象的整个命名空间树。 如果省略 *Address* ，则显示整个命名空间树。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [ACPI 调试](acpi-debugging.md)。

<a name="remarks"></a>备注
-------

此扩展等效于 [**！ amli dns/s**](-amli-dns.md)。

 

 





