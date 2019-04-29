---
title: INF PS2_Inst.NoInterruptInit 节
description: INF PS2_Inst.NoInterruptInit 节
ms.assetid: e84cc7fc-8b17-4119-84f9-12ac888c68aa
keywords:
- INF 文件 WDK 非 HID 键盘/鼠标
- PS2_Inst.NoInterruptInit 部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d699a4005cd977665b74bb4eb293ecf337548bb8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364681"
---
# <a name="inf-ps2instnointerruptinit-section"></a>INF PS2\_Inst.NoInterruptInit 部分





**\[PS2\_Inst.NoInterruptInit\]**
**AddReg** = <em>添加 reg 部分</em>**。AddReg**鼠标类安装程序在如果在本部分中执行指令*禁用*中的条目[INF **PS2\_Inst.NoInterruptInit.Bios**部分](inf-ps2-inst-nointerruptinit-bioses-section.md)与系统 BIOS 版本匹配。

### <a name="entries-and-values"></a>条目和值

<a href="" id="add-reg-section"></a>*add-reg-section*  
指定**AddReg**鼠标类安装程序用于在设备的硬件密钥中设置注册表值的部分。 注册表值确定通过中断或通过轮询系统是否初始化鼠标设备。

### <a href="" id="comments"></a>备注

本节仅与结合使用[INF **PS2\_Inst.NoInterruptInit.Bioses**部分](inf-ps2-inst-nointerruptinit-bioses-section.md)。 本部分的主要用途是指定**AddReg**将注册表值添加到鼠标设备的硬件密钥的部分。

### <a name="add-reg-section-entries"></a>*添加 reg 节条目*

**HKR**,,"**DisableInitializePolledUI**",0x00010001,1 **HKR**,,"**MouseInitializePolled**",0x00010001,1

<a href="" id="disableinitializepolledui"></a>**DisableInitializePolledUI**  
指定 REG\_DWORD 标志，指示是否**快速初始化**属性页上的复选框将提供。 如果**DisableInitializePolledUI**是设置为非零值，该复选框不可用; 否则，复选框才可用。

<a href="" id="mouseinitializedpolled"></a>**MouseInitializedPolled**  
指定 REG\_DWORD 标志，指示系统是否必须轮询设备对其进行初始化。 如果**MouseInitializedPolled**设置为 1，系统轮询的鼠标设备; 否则系统会使用中断。

 

 




