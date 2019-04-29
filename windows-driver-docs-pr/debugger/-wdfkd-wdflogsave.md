---
title: wdfkd.wdflogsave
description: Wdfkd.wdflogsave 扩展保存到事件跟踪日志 (.etl) 文件，您可以通过使用 TraceView 内核模式驱动程序框架 (KMDF) 错误的指定驱动程序日志记录。
ms.assetid: e072d522-a418-4afb-8434-c6355d026770
keywords:
- wdfkd.wdflogsave Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdflogsave
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: edf5e0724182de80f2fdd85f2f0727ae97eb1f47
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323459"
---
# <a name="wdfkdwdflogsave"></a>!wdfkd.wdflogsave


**！ Wdfkd.wdflogsave**扩展将内核模式驱动程序框架 (KMDF) 错误的指定驱动程序日志记录保存到可以通过使用 TraceView 查看的事件跟踪日志 (.etl) 文件。

```dbgcmd
!wdfkd.wdflogsave [DriverName [FileName]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *DriverName*   
可选。 驱动程序的名称。 *DriverName*不得包含.sys 文件扩展名。

<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
可选。 KMDF 错误日志记录将保存到其中的文件的名称。 *文件名*不应包含.etl 文件扩展名。 如果省略*文件名*，KMDF 错误日志记录保存到 DriverName.etl 文件。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

如果省略*DriverName*使用参数，默认驱动程序名称。 使用[ **！ wdfkd.wdfgetdriver** ](-wdfkd-wdfgetdriver.md)扩展来显示默认驱动程序名称，并使用[ **！ wdfkd.wdfsetdriver** ](-wdfkd-wdfsetdriver.md)扩展设置默认驱动程序名称。

 

 





