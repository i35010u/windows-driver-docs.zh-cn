---
title: ndiskd. 微型驱动程序
description: Ndiskd. 微型驱动程序命令显示有关 NDIS 微型端口驱动程序的信息。
keywords:
- ndiskd 微型驱动程序 Windows 调试
ms.date: 06/15/2020
topic_type:
- apiref
api_name:
- ndiskd.minidriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9a792123d058df8e5af42005516fd6bb2c9b7c26
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832869"
---
# <a name="ndiskdminidriver"></a>!ndiskd.minidriver

**！ Ndiskd. 微型驱动程序** 命令显示有关 NDIS 微型端口驱动程序的信息。 如果运行不带参数的此扩展，！ ndiskd 将显示系统上处于活动状态的 NDIS 微型端口驱动程序的列表。

```console
!ndiskd.minidriver [-handle <x>] [-basic] [-miniports] [-devices] [-handlers]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
NDIS 微型端口驱动程序的可选句柄。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span>*-基本*   
显示有关微型端口驱动程序的基本信息。

<span id="_______-miniports______"></span><span id="_______-MINIPORTS______"></span>*-微型端口*   
显示与此小型端口驱动程序关联的微型端口。

<span id="_______-devices______"></span><span id="_______-DEVICES______"></span>*-设备*   
显示与此小型端口驱动程序关联的设备。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span>*-处理程序*   
显示此驱动程序的小型端口处理程序。

## <a name="dll"></a>DLL

Ndiskd.dll

## <a name="examples"></a>示例

输入不带参数的 **！ ndiskd** 命令，以获取系统上所有活动的 NDIS 微型端口驱动程序的列表。 在下面的示例中，查找 kdnic 适配器的句柄 ffffd20d12dec020

```console
1: kd> !ndiskd.minidriver -basic
    ffffd20d173deae0 - tunnel
    ffffd20d12dec020 - kdnic
```

使用 kdnic 适配器的句柄，你现在可以单击该句柄或输入 **！ ndiskd** 命令来查看隧道微型端口驱动程序的详细信息，以及与之关联的微型端口列表。

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

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)
