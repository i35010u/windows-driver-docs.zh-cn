---
title: ndiskd.vc
description: Ndiskd.vc 扩展显示面向连接的 (CoNDIS) 的虚拟连接 (VC)。
ms.assetid: 8F172026-3FBC-4686-A3A4-F54F1A0D08E5
keywords:
- ndiskd.vc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.vc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7e575a83ccd374491fb3ab17c7724d81222b3c84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575177"
---
# <a name="ndiskdvc"></a>!ndiskd.vc


**！ Ndiskd.vc**扩展显示面向连接的 (CoNDIS) 的虚拟连接 (VC)。

```console
!ndiskd.vc [-handle <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 VC 指针的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="remarks"></a>备注
-------

有关的 CoNDIS 详细信息，请参阅[Connection-Oriented NDIS](https://msdn.microsoft.com/windows/hardware/drivers/network/connection-oriented-ndis)。

有关的 CoNDIS 虚拟连接的详细信息，请参阅[虚拟连接](https://msdn.microsoft.com/windows/hardware/drivers/network/virtual-connections)。

<a name="examples"></a>示例
--------

在某些情况下，例如连接到 VPN，因此，运行使用的 CoNDIS **！ ndiskd.vc**将不会显示结果除非您的系统上的微型端口驱动程序已创建并激活的 CoNDIS 虚拟连接。 下面的示例演示从连接到 VPN 网络的计算机的结果。 首先，运行[ **！ ndiskd.netadapter** ](-ndiskd-netadapter.md)不带任何参数，列出在系统上的微型端口和微型端口驱动程序的扩展。 在下面的输出，查找 Marvell AVASTAR 无线 AC 网络控制器网络适配器的微型端口驱动程序。 其句柄是 ffffc804af2e3710。

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

接下来，输入 **！ ndiskd.vc**微型端口驱动程序的句柄，以查看由该微型端口驱动程序打开的虚拟连接命令。

```console
1: kd> !ndiskd.vc ffffc804af2e3710


VIRTUAL CALL

    [Zero-length string]
    Ndis handle        ffffc804af2e3710
    VC Index           0

    AF                 fffff80965fd5888
    Call Flags         [No flags set]
    VC Flags           [Unrecognized flags 04a80100] VC_ACTIVATE_PENDING

    Miniport           fffff80965ffaa20 - [Invalid NetAdapter]
    Miniport Context   fffff80965ffaad0

    Call Manager       fffff80965ff9b50 - [Invalid Open]
    Call Manager Context fffff80965ff9c70

    Client             ffffc804af96fd78 - [Invalid Open]
    Client Context     00003206
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[面向连接的 NDIS](https://msdn.microsoft.com/windows/hardware/drivers/network/connection-oriented-ndis)

[虚拟连接](https://msdn.microsoft.com/windows/hardware/drivers/network/virtual-connections)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

 

 






