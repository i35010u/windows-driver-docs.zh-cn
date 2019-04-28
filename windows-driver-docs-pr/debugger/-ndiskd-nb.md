---
title: ndiskd.nb
description: Ndiskd.nb 扩展显示 NET_BUFFER (NB) 结构的信息。
ms.assetid: 7351264c-4adc-43ac-9eca-41deb3d35983
keywords:
- ndiskd.nb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d7ccf356ba74a48f0d1ea8df2146326b38b67075
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335976"
---
# <a name="ndiskdnb"></a>!ndiskd.nb


**！ Ndiskd.nb**扩展显示有关的信息[ **NET\_缓冲区**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-structure) (NB) 结构。

```console
!ndiskd.nb [-handle <x>] [-verbosity <x>] [-basic] [-chain] [-data] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 地址**NET\_缓冲区**结构。

<span id="_______-verbosity______"></span><span id="_______-VERBOSITY______"></span> *-verbosity*   
要显示的详细信息级别。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
显示有关 NB.的基本信息

<span id="_______-chain______"></span><span id="_______-CHAIN______"></span> *-chain*   
显示与 NB.相关联的所有 MDLs

<span id="_______-data______"></span><span id="_______-DATA______"></span> *-data*   
转储 NB.的实际数据负载

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

**NET\_缓冲区**下面的示例中获取从[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-list-structure)中的示例部分[ **！ ndiskd.nbl** ](-ndiskd-nbl.md)主题。 NB 的句柄是 ffffdf8014952610。

```console
2: kd> !ndiskd.nbl ffffdf80149524a0 -data
NET_BUFFER ffffdf8014952610
```

可以单击**NET\_缓冲区**的句柄或运行 **！ ndiskd.nb-处理**命令以查看其详细信息。

```console
2: kd> !ndiskd.nb ffffdf8014952610
    NB                 ffffdf8014952610    Next NB            0
    Length             0                   Source pool        ffffdf80147e4a40
    First MDL          ffffdf8014a37930    DataOffset         0
    Current MDL        [First MDL]         Current MDL offset 0

    View associated NBL
```

使用 **！ ndiskd.nb-链**命令，请参阅此**NET\_缓冲区**的 MDL 链除了其基本详细信息。 在以下示例中，没有一个 MDL。 其句柄是 ffffdf8014a37930。

```console
2: kd> !ndiskd.nb ffffdf8014952610 -chain
    NB                 ffffdf8014952610    Next NB            0
    Length             0                   Source pool        ffffdf80147e4a40
    First MDL          ffffdf8014a37930    DataOffset         0
    Current MDL        [First MDL]         Current MDL offset 0
        MDL [current]      ffffdf8014a37930    MDL Flags             c
        MappedSystemVa     ffffdf8014bf0024    ByteCount          0n1514
        Process            [System process]    ByteOffset         0n36  
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NET\_BUFFER**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-structure)

[**NET\_BUFFER\_LIST**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-list-structure)

[**!ndiskd.nbl**](-ndiskd-nbl.md)

 

 






