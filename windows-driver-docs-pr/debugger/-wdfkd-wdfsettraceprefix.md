---
title: wdfkd.wdfsettraceprefix
description: Wdfkd.wdfsettraceprefix 扩展设置的跟踪前缀格式字符串。
ms.assetid: dec47b55-4b6a-4ff5-8622-4a377a1903b8
keywords:
- wdfkd.wdfsettraceprefix Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfsettraceprefix
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ecafdceebd73e3ba57857389da8de38bf209148c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323133"
---
# <a name="wdfkdwdfsettraceprefix"></a>!wdfkd.wdfsettraceprefix


**！ Wdfkd.wdfsettraceprefix**扩展设置跟踪前缀格式字符串。

```dbgcmd
!wdfkd.wdfsettraceprefix String
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span> *字符串*   
一个跟踪的前缀字符串。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

跟踪的前缀字符串预置到内核模式驱动程序框架 (KMDF) 错误日志中的每条跟踪消息。 跟踪\_格式\_前缀环境变量也控制跟踪前缀字符串。

由 Microsoft Windows 跟踪工具定义跟踪前缀字符串的格式。 此字符串以及如何自定义它的格式的详细信息，请参阅中的 Windows Driver Kit (WDK) 中的驱动程序开发工具部分的"跟踪消息前缀"主题。

 

 





