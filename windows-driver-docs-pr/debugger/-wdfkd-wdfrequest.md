---
title: wdfkd.wdfrequest
description: Wdfkd. wdfrequest 扩展显示与请求对象关联 (IRP) 指定框架请求对象和 WDM i/o 请求包的相关信息。
keywords:
- wdfkd wdfrequest Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfrequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: edfe6498ebd9725e97f18d6bd7254e071159ba11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833711"
---
# <a name="wdfkdwdfrequest"></a>!wdfkd.wdfrequest


**！ Wdfkd; wdfrequest** 扩展显示与请求对象关联的有关指定框架请求对象和 WDM i/o 请求包 (IRP) 的信息。

```dbgcmd
!wdfkd.wdfrequest Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
框架请求对象的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





