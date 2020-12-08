---
title: INF PS2_Inst.NoInterruptInit 节
description: INF PS2_Inst.NoInterruptInit 节
keywords:
- INF 文件 WDK 非 HID 键盘/鼠标
- PS2_Inst NoInterruptInit 部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ce81498a55c950b10b0e8bb9bc3e62d233b85aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819068"
---
# <a name="inf-ps2_instnointerruptinit-section"></a>INF PS2 \_ 指令. NoInterruptInit 部分





**\[ PS2 \_ 指令. NoInterruptInit \]** 
 **AddReg**  =  <em>add-reg-section</em>**。AddReg** 如果 [INF **PS2 \_ 指令. NoInterruptInit** 部分](inf-ps2-inst-nointerruptinit-bioses-section.md)中的 "*禁用*" 条目与系统 Bios 版本相匹配，则鼠标类安装程序将执行本部分中的指令。

### <a name="entries-and-values"></a>项和值

<a href="" id="add-reg-section"></a>*外接程序-部分*  
指定一个 **AddReg** 节，鼠标类安装程序使用该部分来设置设备硬件密钥中的注册表值。 注册表值确定系统是通过使用中断还是通过轮询来初始化鼠标设备。

### <a name="remarks"></a><a href="" id="comments"></a>注释

本节仅与 [INF **PS2 \_ 指令. NoInterruptInit. Bioses** 节](inf-ps2-inst-nointerruptinit-bioses-section.md)结合使用。 本部分的主要目的是指定将注册表值添加到鼠标设备硬件密钥的 **AddReg** 部分。

### <a name="add-reg-section-entries"></a>*添加注册节条目*

**HKR**，，"**DisableInitializePolledUI**"，0x00010001，1 **HKR**，，"**MouseInitializePolled**"，0x00010001，1

<a href="" id="disableinitializepolledui"></a>**DisableInitializePolledUI**  
指定一个 REG \_ DWORD 标志，该标志指示是否可使用属性页上的 " **快速初始化** " 复选框。 如果将 **DisableInitializePolledUI** 设置为非零值，则此复选框不可用;否则，该复选框可用。

<a href="" id="mouseinitializedpolled"></a>**MouseInitializedPolled**  
指定一个 REG \_ DWORD 标志，该标志指示系统是否必须轮询设备以对其进行初始化。 如果将 **MouseInitializedPolled** 设置为 one，系统会轮询鼠标设备;否则，系统会使用中断。

 

 




