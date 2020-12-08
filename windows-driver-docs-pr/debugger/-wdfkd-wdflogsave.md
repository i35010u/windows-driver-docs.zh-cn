---
title: wdfkd.wdflogsave
description: Wdfkd wdflogsave 扩展将指定驱动程序的 Kernel-Mode Driver Framework (KMDF) 错误日志记录保存到可使用 TraceView 查看的事件跟踪日志 ( .etl) 文件。
keywords:
- wdfkd wdflogsave Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdflogsave
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f5c8f9b8f5bc6571aee824264631cea06f291b4d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795709"
---
# <a name="wdfkdwdflogsave"></a>!wdfkd.wdflogsave


**！ Wdfkd wdflogsave** 扩展将指定驱动程序的 Kernel-Mode driver FRAMEWORK (KMDF) 错误日志记录保存到可使用 TraceView 查看的事件跟踪日志 ( .etl) 文件。

```dbgcmd
!wdfkd.wdflogsave [DriverName [FileName]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span>*DriverName*   
可选。 驱动程序的名称。 *DriverName* 不得包含 .sys 文件扩展名。

<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span>*FileName*   
可选。 应将 KMDF 错误日志记录保存到的文件的名称。 *文件名* 不应包含 .etl 文件扩展名。 如果省略 *FileName*，KMDF 错误日志记录会保存到 DriverName 文件中。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

如果省略 *DriverName* 参数，则使用默认的驱动程序名称。 使用 [**！ wdfkd wdfgetdriver**](-wdfkd-wdfgetdriver.md) 扩展显示默认的驱动程序名称，并使用 [**！ wdfkd**](-wdfkd-wdfsetdriver.md) 扩展名设置默认驱动程序名称。

 

 





