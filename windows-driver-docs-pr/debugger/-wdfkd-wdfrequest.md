---
title: wdfkd.wdfrequest
description: Wdfkd.wdfrequest 扩展显示有关指定的框架请求对象和与请求对象相关联的 WDM I/O 请求数据包 (IRP) 的信息。
ms.assetid: 8b99ec30-ac2b-421d-8b20-bfbd09d41dfb
keywords:
- wdfkd.wdfrequest Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfrequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 784bb0cb42b3726094b018d7f2f6e737c285affa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323385"
---
# <a name="wdfkdwdfrequest"></a>!wdfkd.wdfrequest


**！ Wdfkd.wdfrequest**扩展显示有关指定的框架请求对象并与请求对象相关联的 WDM I/O 请求数据包 (IRP) 的信息。

```dbgcmd
!wdfkd.wdfrequest Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
Framework 请求对象的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





