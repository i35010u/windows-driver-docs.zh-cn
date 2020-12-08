---
title: wdfkd.wdfsettraceprefix
description: Wdfkd. wdfsettraceprefix 扩展设置跟踪前缀格式字符串。
keywords:
- wdfkd wdfsettraceprefix Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfsettraceprefix
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c77a91dcb524835334211474dcec85d370aff7c1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785313"
---
# <a name="wdfkdwdfsettraceprefix"></a>!wdfkd.wdfsettraceprefix


**！ Wdfkd wdfsettraceprefix** 扩展设置跟踪前缀格式字符串。

```dbgcmd
!wdfkd.wdfsettraceprefix String
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span>*字符串*   
跟踪前缀字符串。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

 (KMDF) 错误日志中，将跟踪前缀字符串预置到 Kernel-Mode Driver Framework 中的每个跟踪消息。 跟踪 \_ 格式 \_ 前缀环境变量还控制跟踪前缀字符串。

跟踪前缀字符串的格式由 Microsoft Windows 跟踪工具定义。 有关此字符串的格式以及如何对其进行自定义的详细信息，请参阅 Windows 驱动程序工具包 (WDK) 的 "驱动程序开发工具" 部分中的 "跟踪消息前缀" 主题。

 

 





