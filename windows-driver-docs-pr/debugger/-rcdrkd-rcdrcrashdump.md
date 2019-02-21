---
title: rcdrkd.rcdrcrashdump
description: Rcdrkd.rcdrcrashdump 扩展使用小型转储文件用于显示录制器日志 （如果在日志的小型转储中存在）。
ms.assetid: 61DB0462-31F1-4756-87BB-60188887ACAF
keywords:
- rcdrkd.rcdrcrashdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrcrashdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 300ece52f120062e4aeaad46b549d06a17883b7a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534023"
---
# <a name="rcdrkdrcdrcrashdump"></a>!rcdrkd.rcdrcrashdump


[ **！ Rcdrkd.rcdrcrashdump** ](-usb3kd-device-info.md)扩展用于与小型转储文件显示录制器日志 （如果在日志的小型转储中存在）。

```dbgcmd
!rcdrkd.rcdrcrashdump TraceProviderGuid
!rcdrkd.rcdrcrashdump DriverName
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______TraceProviderGuid______"></span><span id="_______traceproviderguid______"></span><span id="_______TRACEPROVIDERGUID______"></span> *TraceProviderGuid*   
跟踪提供程序的 GUID。 此参数必须包含大括号: {*guid*}

<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *DriverName*   
驱动程序的名称。 可对使用即时跟踪记录器 (IFR) 的驱动程序而不是跟踪提供程序 GUID 的驱动程序名称。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Rcdrkd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[RCDRKD 扩展](rcdrkd-extensions.md)

 

 






