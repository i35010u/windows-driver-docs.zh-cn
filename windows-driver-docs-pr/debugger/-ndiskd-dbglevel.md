---
title: ndiskd.dbglevel
description: Ndiskd dbglevel 扩展显示，并根据需要更改当前的 NDIS 调试级别。 警告 ndiskd 已被 WPP 和驱动程序验证程序取代。
ms.assetid: D134FD03-DABA-4558-A5C3-C365F77BD69A
keywords:
- ndiskd dbglevel Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.dbglevel
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 95ee15b8bdeb654099ece0a7a94827be23cc20e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837597"
---
# <a name="ndiskddbglevel"></a>!ndiskd.dbglevel


**！ Ndiskd dbglevel**扩展显示，并根据需要更改当前的 NDIS 调试级别。

**警告**  
 **！ NDISKD**已被 WPP （Windows 软件跟踪预处理器）和驱动程序验证程序取代。 ！如果目标系统不支持 **！ ndiskd dbglevel**，ndiskd 将为你提供以下警告。

```console
0: kd> !ndiskd.dbglevel
    This target does not support tracing through !ndiskd.dbglevel or
    !ndiskd.dbgsystems.
    Learn how to collect traces with WPP
```

如果单击警告底部的链接，！ ndiskd 将会获得详细信息。

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

 

有关 WPP 的详细信息，请参阅[Wpp 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)。

有关驱动程序验证程序的详细信息，请参阅[驱动程序验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)器。

有关 WMI 跟踪的详细信息，请参阅[Wmi 跟踪扩展（Wmitrace）](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-)。

```console
!ndiskd.dbglevel [-level <str>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-level______"></span><span id="_______-LEVEL______"></span> *-级别*   
调试详细级别。 可能的值为：

-   无-禁用调试跟踪
-   严重-启用要打印的致命错误
-   错误-启用打印错误
-   警告-启用要打印的警告
-   INFO-启用要打印的信息性消息
-   详细-启用要打印的所有调试跟踪

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd

<a name="remarks"></a>备注
-------

此扩展仅适用于已检查的 sys.databases。 若要查看 ndiskd 的生成信息，请运行[ **！** ](-ndiskd-ndis.md)

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展（Ndiskd）** ](ndis-extensions--ndiskd-dll-.md)

[ **！ ndiskd。帮助**](-ndiskd-help.md)

[ **！ ndiskd**](-ndiskd-ndis.md)

[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)

[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)

[WMI 跟踪扩展（Wmitrace）](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-)

 

 






