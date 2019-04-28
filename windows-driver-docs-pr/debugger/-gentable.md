---
title: gentable
description: Gentable 扩展显示 RTL_GENERIC_TABLE。
ms.assetid: acf85ff8-9004-4c8e-b67f-20202c577aab
keywords:
- gentable Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gentable
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cde0ff5119e6eb4848fc825ccbd4aeb1e1857548
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336849"
---
# <a name="gentable"></a>!gentable


**！ Gentable**扩展插件都会显示是 RTL\_泛型\_表。

语法

```dbgcmd
!gentable Address[Flag]
```

## <a name="span-idddkgentabledbgspanspan-idddkgentabledbgspanparameters"></a><span id="ddk__gentable_dbg"></span><span id="DDK__GENTABLE_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的地址的 RTL\_泛型\_表。

<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span> *Flag*   
指定表源。 如果*标志*为 1，使用 AVL 表。 如果*标志*为 0 或省略，将使用非 AVL 表。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

 

 





