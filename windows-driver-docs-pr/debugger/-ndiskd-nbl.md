---
title: ndiskd. nbl
description: Ndiskd. nbl 扩展显示 NET_BUFFER_LIST （NBL）结构的相关信息。
ms.assetid: 1806ac7c-b438-4c28-bab0-1b65dba651ea
keywords:
- ndiskd nbl Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nbl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 99dc87fc578316b3eaf58f04d79aadd78ede8e6a
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534732"
---
# <a name="ndiskdnbl"></a>!ndiskd.nbl


**！ Ndiskd nbl**扩展显示有关[**网络 \_ 缓冲区 \_ 列表**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)（nbl）结构的信息。

```console
    !ndiskd.nbl [-handle <x>] [-basic] [-chain] [-info] [-data] 
    [-netmon] [-capfile <str>] [-launch] [-overwrite] [-log]
    [-stacks] [-NblCurrentOwner]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
必需。 **网络 \_ 缓冲区 \_ 列表**结构的地址。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span>*-基本*   
显示有关 NBL 的基本信息。

<span id="_______-chain______"></span><span id="_______-CHAIN______"></span>*-链*   
显示 NBL 链中的所有 Nbl 和[**NET \_ BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)。

<span id="_______-info______"></span><span id="_______-INFO______"></span>*-info*   
显示与 NBL 相关联的所有带外信息。

<span id="_______-data______"></span><span id="_______-DATA______"></span>*-数据*   
显示 NBL 的实际数据负载。

<span id="_______-netmon______"></span><span id="_______-NETMON______"></span>*-netmon*   
查看 Microsoft 网络监视器中的 NBL 链。

<span id="_______-capfile______"></span><span id="_______-CAPFILE______"></span>*-capfile*   
指定要保存到 netmon 捕获的路径。

<span id="_______-launch______"></span><span id="_______-LAUNCH______"></span>*-启动*   
保存捕获文件后，会自动启动 netmon。

<span id="_______-overwrite______"></span><span id="_______-OVERWRITE______"></span>*-覆盖*   
允许覆盖捕获文件（如果已存在）。

<span id="_______-log______"></span><span id="_______-LOG______"></span>*-日志*   
如果启用了 NBL history 日志记录，则显示 NBL 日志。

<span id="_______-stacks______"></span><span id="_______-STACKS______"></span>*-堆栈*   
包含带有 NBL 日志的调用堆栈（与日志一起使用）。

<span id="_______-NblCurrentOwner______"></span><span id="_______-nblcurrentowner______"></span><span id="_______-NBLCURRENTOWNER______"></span>*-NblCurrentOwner*   
显示 NBL 的当前所有者。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd

<a name="examples"></a>示例
--------

在下面的示例中，已启用 NBL 跟踪，以便从 NBL 日志中提取 NBL 的句柄。 有关 NBL 跟踪和 NBL 日志的详细信息，请参阅[**！ ndiskd. nbllog**](-ndiskd-nbllog.md)。

收集日志时，此示例中的 NBL 由 TCPIP6 协议返回到 WFP 本机 Mac 层轻型筛选器。

```console
2: kd> !ndiskd.nbl ffffdf80149524a0
    NBL                ffffdf80149524a0    Next NBL           NULL
    First NB           ffffdf8014952610    Source             ffffdf80140c71a0 - Microsoft Kernel Debug Network Adapter
    Flags              INDICATED, RETURNED, NBL_ALLOCATED, PROTOCOL_020_0,
                       PROTOCOL_200_0

    Walk the NBL chain                     Dump data payload
    Show out-of-band information
    Review NBL history
```

通过单击上一个示例中的 "转储数据负载" 链接或输入 **！ ndiskd**命令，可以看到此 nbl 的数据有效负载。 在下面的示例中，NBL 仅包含一个**网络 \_ 缓冲区**结构。 若要进一步浏览该**网络 \_ 缓冲区**结构的内容，请运行[**！ ndiskd**](-ndiskd-nb.md)命令及其句柄。

```console
2: kd> !ndiskd.nbl ffffdf80149524a0 -data
NET_BUFFER ffffdf8014952610
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展（Ndiskd）**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**网络 \_ 缓冲区 \_ 列表**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[**网络 \_ 缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)

[**!ndiskd.nbllog**](-ndiskd-nbllog.md)

[**!ndiskd.nb**](-ndiskd-nb.md)

 

 






