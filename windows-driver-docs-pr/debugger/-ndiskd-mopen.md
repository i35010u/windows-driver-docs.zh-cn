---
title: ndiskd.mopen
description: Ndiskd. mopen 扩展显示有关微型端口和协议之间的绑定的信息。
ms.assetid: 439c4647-8f3e-4473-aca8-364b5d2206e9
keywords:
- ndiskd mopen Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.mopen
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 018e4917a2049e81bd74b742f99142140c4c2396
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837590"
---
# <a name="ndiskdmopen"></a>!ndiskd.mopen


**！ Ndiskd mopen**扩展显示有关微型端口和协议之间的绑定的信息。 如果运行不带参数的此扩展，！ ndiskd 将显示 NDIS 微型端口驱动程序和协议驱动程序之间所有打开的绑定的列表。

```console
!ndiskd.mopen [-handle <x>] [-ref] 
```

## <a name="span-idddk__ndiskd_mopen_dbgspanspan-idddk__ndiskd_mopen_dbgspanparameters"></a><span id="ddk__ndiskd_mopen_dbg"></span><span id="DDK__NDISKD_MOPEN_DBG"></span>Parameters


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS 开放式绑定的句柄。

<span id="_______-ref______"></span><span id="_______-REF______"></span> *-ref*   
显示开放绑定的 refcounts。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd

<a name="examples"></a>示例
--------

输入！ ndiskd. mopen 命令获取所有打开的绑定的列表。 在此示例中，查找 Microsoft ISATAP 适配器 \#2 微型端口与 TCPIP6TUNNEL 协议之间的绑定。 它的句柄为 ffff8083e56b8110。

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

现在，你可以单击该句柄或使用句柄输入 **！ ndiskd**命令，该命令使你可以查看有关该打开的绑定的更多详细信息，如其数据路径状态和接收路径信息。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展（Ndiskd）** ](ndis-extensions--ndiskd-dll-.md)

[ **！ ndiskd。帮助**](-ndiskd-help.md)

 

 






