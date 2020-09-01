---
title: ndiskd
description: Ndiskd 扩展显示 NET_BUFFER (NB) 结构的相关信息。
ms.assetid: 7351264c-4adc-43ac-9eca-41deb3d35983
keywords:
- ndiskd Windows 调试
ms.date: 06/15/2020
topic_type:
- apiref
api_name:
- ndiskd.nb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b663a2392abafcde237ccfd6a339bbc4f3c5e018
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216766"
---
# <a name="ndiskdnb"></a>!ndiskd.nb

**！ Ndiskd**扩展显示 (nb) 结构的[**网络 \_ 缓冲区**](../network/net-buffer-structure.md)的相关信息。

```console
!ndiskd.nb [-handle <x>] [-verbosity <x>] [-basic] [-chain] [-data]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
必需。 **网络 \_ 缓冲区**的地址。

<span id="_______-verbosity______"></span><span id="_______-VERBOSITY______"></span>*-详细级别*   
要显示的详细信息的级别。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span>*-基本*   
显示有关 NB 的基本信息。

<span id="_______-chain______"></span><span id="_______-CHAIN______"></span>*-链*   
显示与 NB 关联的所有 MDLs。

<span id="_______-data______"></span><span id="_______-DATA______"></span>*-数据*   
转储 NB 的实际数据有效负载。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

以下示例中的**网络 \_ 缓冲区**是从[**！ ndiskd，Nbl**](-ndiskd-nbl.md)主题的 "示例" 部分的[**net \_ buffer \_ 列表**](../network/net-buffer-list-structure.md)中获取的。 NB 的句柄为 ffffdf8014952610。

```console
2: kd> !ndiskd.nbl ffffdf80149524a0 -data
NET_BUFFER ffffdf8014952610
```

可以单击 **网络 \_ 缓冲区**的句柄，或运行 **！ ndiskd** 命令来查看其详细信息。

```console
2: kd> !ndiskd.nb ffffdf8014952610
    NB                 ffffdf8014952610    Next NB            0
    Length             0                   Source pool        ffffdf80147e4a40
    First MDL          ffffdf8014a37930    DataOffset         0
    Current MDL        [First MDL]         Current MDL offset 0

    View associated NBL
```

使用 **！ ndiskd** 命令查看此 **网络 \_ 缓冲区**的 MDL 链以及其基本详细信息。 在下面的示例中，只有一个 MDL。 它的句柄为 ffffdf8014a37930。

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

## <a name="see-also"></a>另请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0) **](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**网络 \_ 缓冲区**](../network/net-buffer-structure.md)

[**网络 \_ 缓冲区 \_ 列表**](../network/net-buffer-list-structure.md)

[**!ndiskd.nbl**](-ndiskd-nbl.md)