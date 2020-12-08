---
title: wdfkd.wdftraceprtdebug
description: Wdfkd wdftraceprtdebug 扩展启用和禁用 Traceprt.dll 诊断模式，该模式将生成详细的调试信息。
keywords:
- wdfkd wdftraceprtdebug Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdftraceprtdebug
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 985dedd00fe9ea1d486ba21cf028aa58ae6a4400
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823645"
---
# <a name="wdfkdwdftraceprtdebug"></a>!wdfkd.wdftraceprtdebug


**！ Wdfkd wdftraceprtdebug** 扩展启用和禁用 Traceprt.dll 诊断模式，该模式将生成详细的调试信息。

```dbgcmd
!wdfkd.wdftraceprtdebug {on | off}
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______on______"></span><span id="_______ON______"></span>**开启**   
启用 Traceprt.dll 诊断模式。

<span id="_______off______"></span><span id="_______OFF______"></span>**关闭**   
禁用 Traceprt.dll 诊断模式。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

只应在技术支持方向上使用！ wdfkd。

 

 





