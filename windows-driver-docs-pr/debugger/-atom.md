---
title: Atom
description: Atom 扩展插件显示格式化的 atom 表指定 atom 或当前进程的所有原子。
ms.assetid: b4127e4f-a20b-497f-ad84-efea0df0dc80
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
ms.openlocfilehash: dd991ea29e8d290b354662d1d25fe34d0a3013ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336997"
---
# <a name="atom"></a>!atom


**！ Atom**扩展显示格式化的 atom 表指定 atom 或当前进程的所有原子。

```dbgcmd
    !atom [Address] 
```

## <a name="span-idddkatomdbgspanspan-idddkatomdbgspanparameters"></a><span id="ddk__atom_dbg"></span><span id="DDK__ATOM_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示的 atom 的十六进制虚拟地址。 如果省略此参数或指定为零，将显示当前进程的 atom 表。 此表列出了进程的所有原子。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<p>Exts.dll</p>
 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关原子和 atom 表的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 





