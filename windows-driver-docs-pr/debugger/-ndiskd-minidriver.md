---
title: ndiskd. 微型驱动程序
description: Ndiskd. 微型驱动程序命令显示有关 NDIS 微型端口驱动程序的信息。
ms.assetid: CD349B10-8363-4D48-A830-CC9EF5EA75BF
keywords:
- ndiskd 微型驱动程序 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.minidriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be4fa3d8ca7e1d401fc365b98b329c34a016709a
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534924"
---
# <a name="ndiskdminidriver"></a>!ndiskd.minidriver


**！ Ndiskd. 微型驱动程序**命令显示有关 NDIS 微型端口驱动程序的信息。 如果运行不带参数的此扩展，！ ndiskd 将显示系统上处于活动状态的 NDIS 微型端口驱动程序的列表。

```console
!ndiskd.minidriver [-handle <x>] [-basic] [-miniports] [-devices] [-handlers] 
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
NDIS 微型端口驱动程序的句柄。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span>*-基本*   
显示有关微型端口驱动程序的基本信息。

<span id="_______-miniports______"></span><span id="_______-MINIPORTS______"></span>*-微型端口*   
显示与此小型端口驱动程序关联的微型端口。

<span id="_______-devices______"></span><span id="_______-DEVICES______"></span>*-设备*   
显示与此小型端口驱动程序关联的设备。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span>*-处理程序*   
显示此驱动程序的小型端口处理程序。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Ndiskd

<a name="examples"></a>示例
--------

输入不带参数的 **！ ndiskd**命令，以获取系统上所有活动的 NDIS 微型端口驱动程序的列表。 在下面的示例中，查找 kdnic 适配器的句柄 ffffd20d12dec020

```console
1: kd> !ndiskd.minidriver -basic
    ffffd20d173deae0 - tunnel
    ffffd20d12dec020 - kdnic
```

使用 kdnic 适配器的句柄，你现在可以单击该句柄或输入 **！ ndiskd**命令来查看隧道微型端口驱动程序的详细信息，以及与之关联的微型端口列表。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展（Ndiskd）**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

 

 






