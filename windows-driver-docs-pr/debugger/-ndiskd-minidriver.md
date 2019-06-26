---
title: ndiskd.minidriver
description: Ndiskd.minidriver 命令显示有关 NDIS 微型端口驱动程序的信息。
ms.assetid: CD349B10-8363-4D48-A830-CC9EF5EA75BF
keywords:
- ndiskd.minidriver Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.minidriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 725517285a9e0ad45933f3b8a070d49f5f561fda
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365759"
---
# <a name="ndiskdminidriver"></a>!ndiskd.minidriver


**！ Ndiskd.minidriver**命令显示有关 NDIS 微型端口驱动程序的信息。 如果不带任何参数运行此扩展 ！ ndiskd 将显示在系统处于活动状态的 NDIS 微型端口驱动程序的列表。

```console
!ndiskd.minidriver [-handle <x>] [-basic] [-miniports] [-devices] [-handlers] 
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS 微型端口驱动程序的句柄。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
显示有关微型端口驱动程序的基本信息。

<span id="_______-miniports______"></span><span id="_______-MINIPORTS______"></span> *-miniports*   
显示与此微型端口驱动程序相关联的微型端口。

<span id="_______-devices______"></span><span id="_______-DEVICES______"></span> *-devices*   
显示与此微型端口驱动程序相关联的设备。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span> *-handlers*   
显示此驱动程序微型端口处理程序。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Ndiskd.dll

<a name="examples"></a>示例
--------

输入 **！ ndiskd.minidriver**命令不带任何参数来获取所有 NDIS 微型端口驱动程序的列表活动在系统上。 在以下示例中，查找 kdnic 适配器的句柄，ffffd20d12dec020

```console
1: kd> !ndiskd.minidriver -basic
    ffffd20d173deae0 - tunnel
    ffffd20d12dec020 - kdnic
```

为 kdnic 适配器使用句柄，现在可以单击该句柄或输入 **！ ndiskd.minidriver-处理**命令，查看隧道微型端口驱动程序，以及与之关联的微型端口的列表的详细的信息。

```console
1: kd> !ndiskd.minidriver ffffd20d12dec020


MINIPORT DRIVER

    kdnic

    Ndis handle        ffffd20d12dec020    [type it]
    Driver context     fffff80d2fa15100
    DRIVER_OBJECT      ffffd20d12dee540
    Driver image       kdnic.sys
    Registry path      \REGISTRY\MACHINE\SYSTEM\ControlSet001\Services\kdnic
    Reference Count    2
    Flags              [No flags set]


MINIPORTS

    Miniport                                                                    
    ffffd20d12dd71a0 - Microsoft Kernel Debug Network Adapter

    Handlers
    Device objects
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

 

 






