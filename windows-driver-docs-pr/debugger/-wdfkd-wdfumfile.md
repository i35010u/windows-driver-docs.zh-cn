---
title: wdfkd.wdfumfile
description: Wdfkd. wdfumfile 扩展显示有关 UMDF 堆栈内文件的信息。
keywords:
- wdfkd wdfumfile Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumfile
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8baa37cc905c253e19c0d078b31a46ff26d32693
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823625"
---
# <a name="wdfkdwdfumfile"></a>!wdfkd.wdfumfile


**！ Wdfkd wdfumfile** 扩展显示有关 UMDF 堆栈内文件的信息。

```dbgcmd
!wdfkd.wdfumfile Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示其相关信息的 UMDF 内堆栈文件的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作


UMDF 2

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

可以在内核模式调试会话中或在附加到 UMDF 主机进程 ( # A0) 的用户模式调试会话中使用此命令。

此命令显示与用户模式命令 [**！ wudfext**](-wudfext-umfile.md)相同的信息。

 

 





