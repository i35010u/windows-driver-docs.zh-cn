---
title: usbkd.usbhcdlistlogs
description: 'Usbkd. usbhcdlistlogs 命令显示与 USB 端口驱动程序关联的所有功能设备对象 (FDOs) 的列表 ( # A0) 和调试日志。'
keywords:
- usbkd usbhcdlistlogs Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdlistlogs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5c9a91226e7c330666a23855a19d10ca258302a0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818689"
---
# <a name="usbkdusbhcdlistlogs"></a>!usbkd.usbhcdlistlogs


**！ Usbkd usbhcdlistlogs** 命令显示与 USB 端口驱动程序关联的所有功能设备对象 (FDOs) 的列表 ( # A0) 。 该命令还显示所有 EHCI 主机控制器的完整调试日志。

```dbgcmd
!usbkd.usbhcdlistlogs
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

此示例显示 **！ usbhcdlistlogs** 命令输出的一部分。

```dbgcmd
0: kd> !usbkd.usbhcdlistlogs

MINIPORT List @ fffff80001e5bbd0
*flink, blink ffffe00001f48018,ffffe00001f48bd8

[0] entry @: ffffe00001f48010 dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48010
UHCI MINIPORT @ ffffe00001f48010 !drvobj ffffe00002000060 regpkt ffffe00001f48048
02. !devobj ffffe00001ca4050 !usbhcdext ffffe00001ca41a0  HFDO 8086 2938  RHPDO ffffe0000213a050
03. !devobj ffffe00001ca7050 !usbhcdext ffffe00001ca71a0  HFDO 8086 2937  RHPDO ffffe00002140050

[1] entry @: ffffe00001f48bd0 dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0
EHCI MINIPORT @ ffffe00001f48bd0 !drvobj ffffe00001fd33a0 regpkt ffffe00001f48c08
01. !devobj ffffe00001ca1050 !usbhcdext ffffe00001ca11a0  HFDO 8086 293c  RHPDO ffffe0000213c050

LOG@: ffffe00001ca11b8 
>LOG mask = 3ff idx = fff69e8d (28d)
*LOG: ffffe000020191a0  LOGSTART: ffffe00002014000 *LOGEND: ffffe0000201bfe0 # -1 
[ 000] ffffe000020191a0 Tmt0 0000000000000000 0000000000000000 0000000000000000 
[ 001] ffffe000020191c0 _Pop 0000000000000003 0000000000003000 0000000000000000 
...
[ 005] ffffe00002019240 chgZ 0000000000000000 0000000000b7228f 0000000000000000 
[ 006] ffffe00002019260 nes- 0000000000000000 0000000000000000 0000000000000000 
[ 007] ffffe00002019280 nes+ ffffe00001ca2370 ffffe00001ca2370 00000000000ced39 
...
[1014] ffffe00002019060 tmo4 0000000000000000 0000000000000040 ffffe00001ca1c20 
...
[1022] ffffe00002019160 xdw2 ffffe00001ca1b88 ffffe00001ca1050 0000000000000002 
[1023] ffffe00002019180 xdB0 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
```

命令输出显示两个 FDOs，分别表示 UHCI 主机 controlers 和一个表示 EHCI 主机控制器的 FDO。 然后，输出显示一个 EHCI 主机控制器的调试日志。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

