---
title: lockedpages
description: Lockedpages 扩展显示指定进程的驱动程序锁定页。
ms.assetid: a3f70b5f-350c-482f-a172-3abb2b22f408
keywords:
- 驱动程序锁定页
- lockedpages Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lockedpages
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3716e6cfe9eae4d17759c226a1c5147cb2affb4d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569251"
---
# <a name="lockedpages"></a>!lockedpages


**！ Lockedpages**扩展显示指定进程的驱动程序锁定页。

语法

```dbgcmd
!lockedpages [Process]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *Process*   
指定进程。 如果*进程*是省略，使用当前进程。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

<a name="remarks"></a>备注
-------

可以通过按 CTRL + BREAK （在 WinDbg) 或 CTRL + C （中 KD) 来停止执行任何时候。

 

 





