---
title: lockedpages
description: Lockedpages 扩展显示指定进程的驱动程序锁定页面。
keywords:
- 驱动程序-锁定页面
- lockedpages Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lockedpages
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 661ca7a9f99e03fc2cc898d99a04b69f0d3b6eb6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828941"
---
# <a name="lockedpages"></a>!lockedpages


**！ Lockedpages** extension 显示指定进程的驱动程序锁定页面。

语法

```dbgcmd
!lockedpages [Process]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span>*处理*   
指定进程。 如果省略 *进程* ，则使用当前进程。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

<a name="remarks"></a>备注
-------

您可以通过在 WinDbg) 中按 CTRL + BREAK (或在 KD) 中按 CTRL + C (，随时停止执行。

 

 





