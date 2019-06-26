---
title: ndiskd.dbglevel
description: Ndiskd.dbglevel 扩展显示，并根据需要更改当前的 NDIS 调试级别。 警告 ndiskd.dbglevel 具有被取代 WPP 和驱动程序验证程序。
ms.assetid: D134FD03-DABA-4558-A5C3-C365F77BD69A
keywords:
- ndiskd.dbglevel Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.dbglevel
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5dcfce77cc0c94361590aeda3ec1c6ede7b62fe6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364303"
---
# <a name="ndiskddbglevel"></a>!ndiskd.dbglevel


**！ Ndiskd.dbglevel**扩展显示，并根据需要更改当前的 NDIS 调试级别。

**警告**  
 **！ ndiskd.dbglevel**已 WPP （Windows 软件跟踪预处理器） 和驱动程序验证程序被取代。 ！ ndiskd 将显示以下警告如果您的目标系统不支持 **！ ndiskd.dbglevel**。

```console
0: kd> !ndiskd.dbglevel
    This target does not support tracing through !ndiskd.dbglevel or
    !ndiskd.dbgsystems.
    Learn how to collect traces with WPP
```

如果您单击底部的警告，链接 ！ ndiskd 将为你提供详细信息。

```console
0: kd> !ndiskd.help wpptracing
    WPP traces are fast, flexible, and detailed.  Plus, starting with Windows 8
    and Windows Server 2012, you can automatically decode NDIS traces using the
    symbol file.  Just point TraceView (or tracepdb.exe) at NDIS.PDB, and it
    will be able to get all the TMFs it needs to trace NDIS activity.
    
    If you would like traces to be printed in the debugger window, you use the
    !wmitrace extension.  For example, you might enable traces with this:

    !wmitrace.searchpath c:\path\to\TMF\files
    !wmitrace.start ndis -kd
    !wmitrace.enable ndis {DD7A21E6-A651-46D4-B7C2-66543067B869} -level 4 -flag 0x31f3
```

 

有关 WPP 详细信息，请参阅[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)。

有关驱动程序验证程序的详细信息，请参阅[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。

有关 WMI 跟踪的详细信息，请参阅[WMI 跟踪扩展 (Wmitrace.dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-)。

```console
!ndiskd.dbglevel [-level <str>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-level______"></span><span id="_______-LEVEL______"></span> *-level*   
调试详细程度级别。 可能的值为：

-   无-禁用调试跟踪
-   致命错误-启用要打印的致命错误
-   错误-启用要打印的错误
-   警告-启用警告要打印
-   信息-启用要打印的信息性消息
-   详细-启用所有调试跟踪要打印

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="remarks"></a>备注
-------

此扩展适用于仅选中 NDIS.sys。 若要检查 NDIS.sys 的生成信息，请运行[ **！ ndiskd.ndis** ](-ndiskd-ndis.md)扩展。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[ **!ndiskd.ndis**](-ndiskd-ndis.md)

[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)

[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)

[WMI 跟踪扩展 (Wmitrace.dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-)

 

 






