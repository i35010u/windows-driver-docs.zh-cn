---
title: atom
description: Atom 扩展为指定的 atom 或当前进程的所有原子显示格式化的 atom 表。
keywords:
- atom Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- atom
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 620c3f4c0d99207a2ad31071a07f61826ae8d134
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800001"
---
# <a name="atom"></a>!atom


**！ Atom** extension 为指定的 atom 或当前进程的所有原子显示格式化的 atom 表。

```dbgcmd
    !atom [Address] 
```

## <a name="span-idddk__atom_dbgspanspan-idddk__atom_dbgspanparameters"></a><span id="ddk__atom_dbg"></span><span id="DDK__ATOM_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示的 atom 的十六进制虚拟地址。 如果省略此参数或指定零，则显示当前进程的 atom 表。 此表列出了进程的所有原子。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<p>Exts.dll</p>
 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关原子和 atom 表的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 





