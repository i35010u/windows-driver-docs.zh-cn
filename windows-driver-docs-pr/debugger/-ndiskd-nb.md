---
title: ndiskd
description: Ndiskd 扩展显示有关 NET_BUFFER （NB）结构的信息。
ms.assetid: 7351264c-4adc-43ac-9eca-41deb3d35983
keywords:
- ndiskd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7fb01044dde6b95e312f1de17561d5ac9515c3b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826649"
---
# <a name="ndiskdnb"></a>!ndiskd.nb


**！ Ndiskd**扩展显示[**NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure) （nb）结构的相关信息。

```console
!ndiskd.nb [-handle <x>] [-verbosity <x>] [-basic] [-chain] [-data] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 **NET\_缓冲区**结构的地址。

<span id="_______-verbosity______"></span><span id="_______-VERBOSITY______"></span> *-详细级别*   
要显示的详细信息的级别。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-基本*   
显示有关 NB 的基本信息。

<span id="_______-chain______"></span><span id="_______-CHAIN______"></span> *-链式*   
显示与 NB 关联的所有 MDLs。

<span id="_______-data______"></span><span id="_______-DATA______"></span> *-数据*   
转储 NB 的实际数据有效负载。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd

<a name="examples"></a>示例
--------

以下示例中的**net\_缓冲区**是从[ **！ ndiskd nbl**](-ndiskd-nbl.md)主题的 "示例" 部分中的[**net\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)中获取的。 NB 的句柄为 ffffdf8014952610。

```console
2: kd> !ndiskd.nbl ffffdf80149524a0 -data
NET_BUFFER ffffdf8014952610
```

可以单击**NET\_缓冲区**的句柄，或运行 **！ ndiskd**命令来查看其详细信息。

```console
2: kd> !ndiskd.nb ffffdf8014952610
    NB                 ffffdf8014952610    Next NB            0
    Length             0                   Source pool        ffffdf80147e4a40
    First MDL          ffffdf8014a37930    DataOffset         0
    Current MDL        [First MDL]         Current MDL offset 0

    View associated NBL
```

使用 **！ ndiskd**命令查看此**网络\_缓冲区**的 MDL 链以及其基本详细信息。 在下面的示例中，只有一个 MDL。 它的句柄为 ffffdf8014a37930。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展（Ndiskd）** ](ndis-extensions--ndiskd-dll-.md)

[ **！ ndiskd。帮助**](-ndiskd-help.md)

[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)

[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[ **！ ndiskd. nbl**](-ndiskd-nbl.md)

 

 






