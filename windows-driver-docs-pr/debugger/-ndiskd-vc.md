---
title: ndiskd.vc
description: Ndiskd.vc 扩展显示) 虚拟连接 (VC) 的 Connection-Oriented (CoNDIS。
keywords:
- ndiskd.vc Windows 调试
ms.date: 06/26/2020
topic_type:
- apiref
api_name:
- ndiskd.vc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f6bbd63ce5a494f73406eb95b280b3910cf78713
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813331"
---
# <a name="ndiskdvc"></a>!ndiskd.vc

**！ Ndiskd.vc** 扩展显示) 虚拟连接 (vc) 的 Connection-Oriented (CoNDIS。

```console
!ndiskd.vc -handle <x>
```

## <a name="parameters"></a>参数

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
必需。 VC 指针的句柄。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="remarks"></a>备注

有关 CoNDIS 的详细信息，请参阅 [面向连接的 NDIS](../network/connection-oriented-ndis.md)。

有关 CoNDIS 虚拟连接的详细信息，请参阅 [虚拟连接](../network/virtual-connections.md)。

### <a name="examples"></a>示例

CoNDIS 在某些情况下使用，例如连接到 VPN，因此，如果系统中的微型端口驱动程序已创建并激活 CoNDIS 虚拟连接，则运行 **！ ndiskd.vc** 将不会显示结果。 以下示例显示了连接到 VPN 网络的计算机的结果。 首先，运行不带参数的 [**！ get-netadapter**](-ndiskd-netadapter.md) 扩展，以查看系统上的微型端口和微型端口驱动程序的列表 ndiskd。 在下面的输出中，查找 Marvell AVASTAR 无线-AC 网络控制器网络适配器的微型端口驱动程序。 它的句柄为 ffffc804af2e3710。

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

接下来，使用微型端口驱动程序的句柄输入 **！ ndiskd.vc** 命令，以查看由该微型端口驱动程序打开的虚拟连接。

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

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[面向连接的 NDIS](../network/connection-oriented-ndis.md)

[虚拟连接](../network/virtual-connections.md)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)
