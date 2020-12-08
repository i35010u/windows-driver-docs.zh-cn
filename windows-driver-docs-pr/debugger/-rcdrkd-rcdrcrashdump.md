---
title: rcdrkd.rcdrcrashdump
description: 如果日志存在于小型转储) 中，则使用小型转储文件来显示录像机日志 (。
keywords:
- rcdrkd rcdrcrashdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrcrashdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d41510d3ee9ab17c8b77c86094f7ffaf86c1a9e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837584"
---
# <a name="rcdrkdrcdrcrashdump"></a>!rcdrkd.rcdrcrashdump


如果日志存在于小型转储) 中，则将 [**！ rcdrkd**](-usb3kd-device-info.md) 扩展名与小型转储文件一起用于显示记录器日志 (。

```dbgcmd
!rcdrkd.rcdrcrashdump TraceProviderGuid
!rcdrkd.rcdrcrashdump DriverName
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______TraceProviderGuid______"></span><span id="_______traceproviderguid______"></span><span id="_______TRACEPROVIDERGUID______"></span>*TraceProviderGuid*   
跟踪提供程序的 GUID。 此参数必须包括大括号： {*guid*}

<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span>*DriverName*   
驱动程序的名称。 对于使用即时 Trace 录像机 (IFR) 的驱动程序，可以使用驱动程序名称，而不是跟踪提供程序 GUID。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Rcdrkd.dll

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[RCDRKD 扩展](rcdrkd-extensions.md)

 

 






