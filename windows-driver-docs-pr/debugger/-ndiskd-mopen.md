---
title: ndiskd.mopen
description: Ndiskd.mopen 扩展显示有关微型端口和协议之间的绑定信息。
ms.assetid: 439c4647-8f3e-4473-aca8-364b5d2206e9
keywords:
- ndiskd.mopen Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.mopen
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd991b6da9ab80ece3a88a81410effc9099a4bb6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336009"
---
# <a name="ndiskdmopen"></a>!ndiskd.mopen


**！ Ndiskd.mopen**扩展显示微型端口和协议之间的绑定有关的信息。 如果不带任何参数运行此扩展 ！ ndiskd 将显示所有打开的 NDIS 微型端口驱动程序和协议驱动程序之间的绑定的列表。

```console
!ndiskd.mopen [-handle <x>] [-ref] 
```

## <a name="span-idddkndiskdmopendbgspanspan-idddkndiskdmopendbgspanparameters"></a><span id="ddk__ndiskd_mopen_dbg"></span><span id="DDK__NDISKD_MOPEN_DBG"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS 的句柄打开绑定。

<span id="_______-ref______"></span><span id="_______-REF______"></span> *-ref*   
显示 refcounts 打开绑定。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

输入 ！ ndiskd.mopen 命令来获取所有打开的绑定的列表。 在此示例中，查找 Microsoft ISATAP 适配器之间的绑定\#2 微型端口和 TCPIP6TUNNEL 协议。 其句柄是 ffff8083e56b8110。

```console
3: kd> !ndiskd.mopen
Open ffff8083e56b8110
  Miniport: ffff8083e02ce1a0 - Microsoft ISATAP Adapter #2
  Protocol: ffff8083e1a95c00 - TCPIP6TUNNEL

Open ffff8083e11902c0
  Miniport: ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
  Protocol: ffff8083e3e8f6b0 - RSPNDR

Open ffff8083e55f3010
  Miniport: ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
  Protocol: ffff8083e0114730 - NDISUIO

Open ffff8083e15537d0
  Miniport: ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
  Protocol: ffff8083e3e90800 - LLTDIO

Open ffff8083e3926010
  Miniport: ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
  Protocol: ffff8083e3e90c10 - MSLLDP

Open ffff8083e0c565a0
  Miniport: ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
  Protocol: ffff8083e11cec10 - TCPIP

Open ffff8083e504c770
  Miniport: ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
  Protocol: ffff8083e19bfc10 - TCPIP6
```

现在，你可以单击句柄上或使用该句柄输入 **！ ndiskd.mopen-处理**命令，这样就可以查看有关其数据路径状态如打开绑定的详细信息和接收路径信息。

```console
3: kd> !ndiskd.mopen ffff8083e56b8110


OPEN

    Ndis handle        ffff8083e56b8110
    Flags              [No flags set]
    References         1                   Show detail
    Source             1
    Datapath state     Running

    Protocol           ffff8083e1a95c00 - TCPIP6TUNNEL
    Protocol context   ffff8083e15b62e0

    Miniport           ffff8083e02ce1a0 - Microsoft ISATAP Adapter #2
    Miniport context   ffff8083e0772010


RECEIVE PATH

    Packet filter      [No flags set]
    Frame Type(s)      0x86dd
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

 

 






