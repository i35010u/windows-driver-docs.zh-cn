---
title: ndiskd 协议
description: Ndiskd 命令显示有关 NDIS 协议驱动程序的信息。
keywords:
- ndiskd Windows 调试
ms.date: 06/26/2020
topic_type:
- apiref
api_name:
- ndiskd.protocol
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4cb5c55f846b6f932df007c3f17b3995dfc87767
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836905"
---
# <a name="ndiskdprotocol"></a>!ndiskd.protocol

**！ Ndiskd** 命令显示有关 NDIS 协议驱动程序的信息。 如果运行不带参数的此扩展，！ ndiskd 将显示系统上处于活动状态的 NDIS 协议驱动程序的列表。

```console
!ndiskd.protocol [-handle <x>] [-findname <any>] 
```

## <a name="parameters"></a>参数

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
NDIS 协议的可选句柄。

<span id="_______-findname______"></span><span id="_______-FINDNAME______"></span>*-system.windows.frameworkelement.findname*   
按名称前缀筛选协议。

## <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

输入 **！ ndiskd** 命令，以查看所有 NDIS 协议的列表、它们的句柄和微型端口 (（如果) 有）的绑定。 在下面的示例中，查找 TCPIP6TUNNEL 协议的句柄 ffff8083e1a95c00。

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

在协议的句柄中，现在可以输入或输入 **！ ndiskd** 命令来查看该协议的信息，例如绑定到它的微型端口的句柄。

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

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)
