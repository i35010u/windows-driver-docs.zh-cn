---
title: ndiskd.af
description: Ndiskd.af 扩展显示面向连接的 NDIS （CoNDIS）地址系列（AF）。
ms.assetid: 737AB46E-DFAA-42D6-A9BD-B7223167D0DD
keywords:
- ndiskd.af Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.af
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dd706d7c6be28490605034067d1b7b1024037c4a
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534234"
---
# <a name="ndiskdaf"></a>!ndiskd.af


**！ Ndiskd.af** Extension 显示面向连接的 NDIS （CoNDIS）地址系列（af）。

```console
!ndiskd.af [-handle <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
必需。 CoNDIS 地址族的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd

<a name="remarks"></a>注解
-------

有关 CoNDIS 的详细信息，请参阅[面向连接的 NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/connection-oriented-ndis)。

有关 CoNDIS 地址系列的详细信息，请参阅[地址系列](https://docs.microsoft.com/windows-hardware/drivers/network/address-families)。

<a name="examples"></a>示例
--------

CoNDIS 在某些情况下使用，例如连接到 VPN，因此，如果系统中的微型端口驱动程序已创建并激活 CoNDIS 虚拟连接，则运行 **！ ndiskd.af**将不会显示结果。 以下示例显示了连接到 VPN 网络的计算机的结果。 首先，运行不带参数的[**！ get-netadapter**](-ndiskd-netadapter.md)扩展，以查看系统上的微型端口和微型端口驱动程序的列表 ndiskd。 在下面的输出中，查找 Marvell AVASTAR 无线-AC 网络控制器网络适配器的微型端口驱动程序。 它的句柄为 ffffc804af2e3710。

```console
1: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffc804af2e3710   ffffc804b9e6f1a0    Marvell AVASTAR Wireless-AC Network Controller
    ffffc804b99b9020   ffffc804b9c301a0    WAN Miniport (Network Monitor)
    ffffc804b99b9020   ffffc804b9c2a1a0    WAN Miniport (IPv6)
    ffffc804b99b9020   ffffc804b8a8a1a0    WAN Miniport (IP)
    ffffc804ae9d7020   ffffc804b9ceb1a0    WAN Miniport (PPPOE)
    ffffc804b9ca5900   ffffc804b9e601a0    WAN Miniport (PPTP)
    ffffc804b99dc720   ffffc804b99b01a0    WAN Miniport (L2TP)
    ffffc804b86581b0   ffffc804b9c6c1a0    WAN Miniport (IKEv2)
    ffffc804ad4a7250   ffffc804b99651a0    WAN Miniport (SSTP)
    ffffc804b11c4020   ffffc804b85821a0    Microsoft ISATAP Adapter
    ffffc804b11c4020   ffffc804b71731a0    Microsoft ISATAP Adapter #2
    ffffc804ad725020   ffffc804b05e71a0    Surface Ethernet Adapter #2
    ffffc804b0bf0020   ffffc804b0c011a0    Bluetooth Device (Personal Area Network)
    ffffc804aef695e0   ffffc804aed331a0    TAP-Windows Adapter V9
```

接下来，使用微型端口驱动程序的句柄输入 **！ ndiskd.af**命令，以查看此微型端口驱动程序的地址族，该地址族充当面向连接的客户端。

```console
1: kd> !ndiskd.af ffffc804af2e3710


ADDRESS FAMILY

    Ndis handle        ffffc804af2e3710
    Flags              [Unrecognized flags 399b9020] AF_CLOSING
    References         ffffc804
    Close Requested?   0

    Miniport           0 - [Unreadable NetAdapter]

    Call Manager       ffffc804b90a4ac0 - [Invalid Open]
    Call Manager Context 007a0078

    Client             00060000 - [Unreadable Open]
    Client Context     ffffc804af2e3888


CLIENT HANDLERS

    Client Handler                         Function pointer   Symbol (if available)
    ClCreateVcHandler                      fffff80965fd5888   mrvlpcie8897!Globals+8
    ClDeleteVcHandler                      [None]
    ClRequestHandler                       ffffc804af96fd78
    ClRequestCompleteHandler               ffffc804af96fd78
    ClOpenAfCompleteHandler                [None]
    ClCloseAfCompleteHandler               [None]
    ClRegisterSapCompleteHandler           000132060098028a
    ClDeregisterSapCompleteHandler         [None]
    ClMakeCallCompleteHandler              fffff80965ff9ec0   wdiwifi!MPWrapperSetOptions
    ClCloseCallCompleteHandler             fffff80965ff9c70   wdiwifi!MPWrapperHalt
    ClModifyCallQoSCompleteHandler         fffff80965ff9b50   wdiwifi!MPWrapperInitializeEx
    ClAddPartyCompleteHandler              fffff80965e71a08   mrvlpcie8897!MPUnload
    ClDropPartyCompleteHandler             fffff80965ffa070   wdiwifi!MPWrapperPause
    ClIncomingDropPartyHandler             fffff80965ffaa20   wdiwifi!MPWrapperReturnNetBufferLists
    ClIncomingCallHandler                  fffff80965ffa1e0   wdiwifi!MPWrapperRestart
    ClCallConnectedHandler                 fffff80965ffaad0   wdiwifi!MPWrapperCancelSendNetBufferLists
    ClIncomingCloseCallHandler             fffff80965ffa870   wdiwifi!MPWrapperSendNetBufferLists
    ClIncomingCallQoSChangeHandler         fffff80965ffa610   wdiwifi!MPWrapperOidRequest
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展（Ndiskd）**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[面向连接的 NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/connection-oriented-ndis)

[地址系列](https://docs.microsoft.com/windows-hardware/drivers/network/address-families)

 

 






