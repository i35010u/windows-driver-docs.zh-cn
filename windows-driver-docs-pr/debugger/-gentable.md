---
title: gentable
description: Gentable 扩展显示 RTL_GENERIC_TABLE。
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
ms.openlocfilehash: 2a53a9137f3eaf7cf50359affeae07797f444570
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824799"
---
# <a name="gentable"></a>!gentable


**！ Gentable** EXTENSION 显示 RTL \_ 泛型 \_ 表。

语法

```dbgcmd
!gentable Address[Flag]
```

## <a name="span-idddk__gentable_dbgspanspan-idddk__gentable_dbgspanparameters"></a><span id="ddk__gentable_dbg"></span><span id="DDK__GENTABLE_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 RTL 泛型表的地址 \_ \_ 。

<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span>*标志*   
指定表源。 如果 *标志* 为1，则使用 AVL 表。 如果 *标志* 为0或省略，则使用非 AVL 表。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

 

 





