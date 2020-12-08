---
title: INF PS2_Inst.NoInterruptInit.Bioses 节
description: INF PS2_Inst.NoInterruptInit.Bioses 节
keywords:
- INF 文件 WDK 非 HID 键盘/鼠标
- PS2_Inst. NoInterruptInit. Bioses 部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf036dbea3267e06394ca7f04aba462da708289c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838041"
---
# <a name="inf-ps2_instnointerruptinitbioses-section"></a>INF PS2 \_ 指令. NoInterruptInit. Bioses 部分





**\[PS2 \_ 指令. NoInterruptInit. Bioses\]**

*禁用* =*disable-string* 鼠标类安装程序将检查 d *i)* 是否为 **HKLM \\ 硬件 \\ 描述 \\ 系统 \\ SystemBiosVersion** 字符串值的子字符串。 如果是，则类安装程序将执行在 [INF PS2 \_ 指令. NoInterruptInit 部分](inf-ps2-inst-nointerruptinit-section.md)中指定的 inf 指令。

### <a name="entries-and-values"></a>项和值

<a href="" id="disable"></a>*禁用*  
设置为 d *i)* 值。

<a href="" id="disable-string"></a>*disable-string*  
指定 **HKLM \\ 硬件 \\ 描述 \\ 系统 \\ SYSTEMBIOSVERSION** 中唯一标识系统 BIOS 的子字符串。

### <a name="remarks"></a><a href="" id="comments"></a>注释

本节仅用于 PS/2 鼠标设备，并且仅与 [INF **PS2 \_ 指令. NoInterruptInit** 部分](inf-ps2-inst-nointerruptinit-section.md)结合使用。

 

 




