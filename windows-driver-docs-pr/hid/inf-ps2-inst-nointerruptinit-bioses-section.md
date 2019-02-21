---
title: INF PS2_Inst.NoInterruptInit.Bioses 部分
description: INF PS2_Inst.NoInterruptInit.Bioses 部分
ms.assetid: 2bf1dc0f-00b6-4f4a-99f0-e9843fe6e66b
keywords:
- INF 文件 WDK 非 HID 键盘/鼠标
- PS2_Inst.NoInterruptInit.Bioses 部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7c36898c220502cac53e641a2b47225d719393a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543303"
---
# <a name="inf-ps2instnointerruptinitbioses-section"></a>INF PS2\_Inst.NoInterruptInit.Bioses 部分





**\[PS2\_Inst.NoInterruptInit.Bioses\]**

*禁用*=*禁用字符串*鼠标类安装程序将检查如果 d*isable 字符串*的字符串值的子字符串**HKLM\\硬件\\描述\\系统\\SystemBiosVersion**。 如果是，在类安装程序执行中指定的 INF 指令[INF PS2\_Inst.NoInterruptInit 部分](inf-ps2-inst-nointerruptinit-section.md)。

### <a name="entries-and-values"></a>条目和值

<a href="" id="disable"></a>*禁用*  
设置为 d*isable 字符串*值。

<a href="" id="disable-string"></a>*disable-string*  
指定子字符串在**HKLM\\硬件\\说明\\系统\\SystemBiosVersion**用于唯一标识系统 BIOS。

### <a href="" id="comments"></a>备注

仅使用 ps/2 鼠标设备和仅在与组合中使用此部分[INF **PS2\_Inst.NoInterruptInit**部分](inf-ps2-inst-nointerruptinit-section.md)。

 

 




