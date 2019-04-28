---
title: ndiskd.protocol
description: Ndiskd.protocol 命令显示有关 NDIS 协议驱动程序的信息。
ms.assetid: c1d349d5-b0ba-4665-a399-1bc5cd55dde6
keywords:
- ndiskd.protocol Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.protocol
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a4ec826a3450d527d28ea5735cdf1f0fc7809f18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335910"
---
# <a name="ndiskdprotocol"></a>!ndiskd.protocol


**！ Ndiskd.protocol**命令显示有关 NDIS 协议驱动程序的信息。 如果不带任何参数运行此扩展 ！ ndiskd 将显示在系统处于活动状态的 NDIS 协议驱动程序的列表。

```console
!ndiskd.protocol [-handle <x>] [-findname <any>] 
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS 协议的句柄。

<span id="_______-findname______"></span><span id="_______-FINDNAME______"></span> *-findname*   
按名称前缀筛选的协议。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Ndiskd.dll

<a name="examples"></a>示例
--------

输入 **！ ndiskd.protocol**命令以列出所有 NDIS 协议，其句柄，并打开到微型端口的绑定 （如果有）。 在以下示例中，查找 TCPIP6TUNNEL 协议的句柄，ffff8083e1a95c00。

```console
3: kd> !ndiskd.protocol
ffff8083e0114730 - NDISUIO
  ffff8083e55f3010 - Microsoft Kernel Debug Network Adapter

ffff8083e3e90c10 - MSLLDP
  ffff8083e3926010 - Microsoft Kernel Debug Network Adapter

ffff8083e3e98c10 - WANARPV6

ffff8083e3e97010 - WANARP

ffff8083e3e8f6b0 - RSPNDR
  ffff8083e11902c0 - Microsoft Kernel Debug Network Adapter

ffff8083e3e90800 - LLTDIO
  ffff8083e15537d0 - Microsoft Kernel Debug Network Adapter

ffff8083e1a9ac10 - RDMANDK

ffff8083e1a95c00 - TCPIP6TUNNEL
  ffff8083e56b8110 - Microsoft ISATAP Adapter #2

ffff8083e19bec10 - TCPIPTUNNEL

ffff8083e19bfc10 - TCPIP6
  ffff8083e504c770 - Microsoft Kernel Debug Network Adapter

ffff8083e11cec10 - TCPIP
  ffff8083e0c565a0 - Microsoft Kernel Debug Network Adapter
```

提供的协议的句柄，现在可以输入可以单击该句柄，或输入 **！ ndiskd.protocol-处理**命令以查看有关该协议，例如绑定到该微型端口的句柄的信息。

```console
3: kd> !ndiskd.protocol ffff8083e1a95c00


PROTOCOL

    TCPIP6TUNNEL

    Ndis handle        ffff8083e1a95c00
    Ndis API version   v6.40
    Driver context     fffff80e2e4f9de0
    Driver version     v0.0
    Reference count    2
    Flags              [No flags set]
    Driver image       [Not available]     Why not?


BINDINGS

    Open               Miniport            Miniport Name                        
    ffff8083e56b8110   ffff8083e02ce1a0    Microsoft ISATAP Adapter #2


HANDLERS

    Protocol handler                       Function pointer   Symbol (if available)
    BindAdapterHandlerEx                   fffff80e2e3baab0  bp
    UnbindAdapterHandlerEx                 fffff80e2e3c1c80  bp
    OpenAdapterCompleteHandlerEx           fffff80e2e4bc940  bp
    CloseAdapterCompleteHandlerEx          fffff80e2e3d19b0  bp
    NetPnPEventHandler                     fffff80e2e3bb140  bp
    UninstallHandler                       [None]
    SendNetBufferListsCompleteHandler      fffff80e2e3919a0  bp
    ReceiveNetBufferListsHandler           fffff80e2e3918a0  bp
    StatusHandlerEx                        fffff80e2e3a9550  bp
    OidRequestCompleteHandler              fffff80e2e398120  bp
    DirectOidRequestCompleteHandler        fffff80e2e398120  bp
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

 

 






