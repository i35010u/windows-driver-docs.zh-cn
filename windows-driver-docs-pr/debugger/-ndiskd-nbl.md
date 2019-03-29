---
title: ndiskd.nbl
description: Ndiskd.nbl 扩展显示 NET_BUFFER_LIST (NBL) 结构的信息。
ms.assetid: 1806ac7c-b438-4c28-bab0-1b65dba651ea
keywords:
- ndiskd.nbl Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nbl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6f946a89a779c1ce344f4091d2df52494b3564c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565833"
---
# <a name="ndiskdnbl"></a>!ndiskd.nbl


**！ Ndiskd.nbl**扩展显示有关的信息[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-list-structure) (NBL) 结构。

```console
    !ndiskd.nbl [-handle <x>] [-basic] [-chain] [-info] [-data] 
    [-netmon] [-capfile <str>] [-launch] [-overwrite] [-log]
    [-stacks] [-NblCurrentOwner]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 地址**NET\_缓冲区\_列表**结构。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
显示有关 NBL 的基本信息。

<span id="_______-chain______"></span><span id="_______-CHAIN______"></span> *-chain*   
显示所有功能的 Nbl 并[ **NET\_缓冲区**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-structure)NBL 链中的 s。

<span id="_______-info______"></span><span id="_______-INFO______"></span> *-info*   
显示与 NBL 相关联的所有带外信息。

<span id="_______-data______"></span><span id="_______-DATA______"></span> *-data*   
显示 NBL 的实际数据负载。

<span id="_______-netmon______"></span><span id="_______-NETMON______"></span> *-netmon*   
Microsoft 网络监视器中查看 NBL 链。

<span id="_______-capfile______"></span><span id="_______-CAPFILE______"></span> *-capfile*   
指定 netmon 捕获保存到其中的路径。

<span id="_______-launch______"></span><span id="_______-LAUNCH______"></span> *-launch*   
保存捕获文件后将自动启动 netmon.exe。

<span id="_______-overwrite______"></span><span id="_______-OVERWRITE______"></span> *-overwrite*   
允许覆盖捕获文件，如果它已存在。

<span id="_______-log______"></span><span id="_______-LOG______"></span> *-log*   
如果启用了 NBL 历史记录日志记录，显示了 NBL 日志。

<span id="_______-stacks______"></span><span id="_______-STACKS______"></span> *-stacks*   
包括与 NBL 日志 （使用带-日志） 的调用堆栈。

<span id="_______-NblCurrentOwner______"></span><span id="_______-nblcurrentowner______"></span><span id="_______-NBLCURRENTOWNER______"></span> *-NblCurrentOwner*   
显示的当前所有者的 NBL。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

在以下示例中，已启用 NBL 跟踪 NBL NBL 日志中提取一个句柄。 有关 NBL 跟踪的 NBL 日志的详细信息，请参阅[ **！ ndiskd.nbllog**](-ndiskd-nbllog.md)。

日志收集时，在此示例中 NBL 到 WFP 本机 Mac 层轻型筛选器返回的 TCPIP6 协议。

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

通过单击"转储数据有效负载"链接上一示例中，或输入 **！ ndiskd.nbl-处理的数据**命令时，您可以看到此 NBL 的数据有效负载。 以下示例中，在 NBL 只包含一个**NET\_缓冲区**结构。 若要进一步探索的内容**NET\_缓冲区**结构，运行[ **！ ndiskd.nb-处理**](-ndiskd-nb.md)命令和其句柄。

```console
2: kd> !ndiskd.nbl ffffdf80149524a0 -data
NET_BUFFER ffffdf8014952610
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NET\_BUFFER\_LIST**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-list-structure)

[**NET\_BUFFER**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-structure)

[**!ndiskd.nbllog**](-ndiskd-nbllog.md)

[**!ndiskd.nb**](-ndiskd-nb.md)

 

 






