---
title: wdfkd.wdftraceprtdebug
description: Wdfkd.wdftraceprtdebug 扩展启用和禁用 Traceprt.dll 诊断模式下，它生成详细的调试信息。
ms.assetid: e12e0ff1-fc27-4d95-b48a-73cab8f1e363
keywords:
- wdfkd.wdftraceprtdebug Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdftraceprtdebug
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5957a4d446f374c04eb0bed17527bf17d8a06975
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563241"
---
# <a name="wdfkdwdftraceprtdebug"></a>!wdfkd.wdftraceprtdebug


**！ Wdfkd.wdftraceprtdebug**扩展启用和禁用 Traceprt.dll 诊断模式下，它生成详细的调试信息。

```dbgcmd
!wdfkd.wdftraceprtdebug {on | off}
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______on______"></span><span id="_______ON______"></span> **on**   
启用 Traceprt.dll 诊断模式。

<span id="_______off______"></span><span id="_______OFF______"></span> **off**   
禁用 Traceprt.dll 诊断模式。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

应使用 ！ wdfkd.wdftraceprtdebug 扩展仅在技术支持的方向。

 

 





