---
title: wdfkd.wdfumirps
description: Wdfkd. wdfumirps 扩展会在隐式进程中显示 (UM Irp) 挂起的用户模式 i/o 请求包的列表。
keywords:
- wdfkd wdfumirps Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumirps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 656a427aaf565afdb354e702d99fbccda1ebb1e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823621"
---
# <a name="wdfkdwdfumirps"></a>!wdfkd.wdfumirps


**！ Wdfkd wdfumirps** 在 [隐式进程](controlling-threads-and-processes.md)中显示 (UM irp) 挂起用户模式 i/o 请求包的列表。

```dbgcmd
!wdfkd.wdfumirps NumberOfIrps Flags
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______NumberOfIrps______"></span><span id="_______numberofirps______"></span><span id="_______NUMBEROFIRPS______"></span>*NumberOfIrps*   
可选。 指定要显示其相关信息的挂起的 UM Irp 的数目。 如果 *NumberOfIrps* 是星号 (\*) 或被省略，则将显示所有 UM irp。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 指定要显示的信息的类型。 *标志* 可以是以下位的任意组合。 默认值为0x01。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>位 0 (0x01)   
显示有关挂起的 Irp 的详细信息。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作


UMDF 2

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

可以在内核模式调试会话中或在附加到 UMDF 主机进程 ( # A0) 的用户模式调试会话中使用此命令。

此命令显示与用户模式命令 [**！ wudfext**](-wudfext-umirps.md)相同的信息。

您可以使用 [**！进程**](-process.md) 获取所有 umdf 主机进程的列表，并且可以使用 [**. 进程**](-process--set-process-context-.md) 将隐式进程设置为一个 umdf 主机进程。 有关详细示例，请参阅 [**！ wdfkd. wdfumdevstacks**](-wdfkd-wdfumdevstacks.md)。

下面是 **！ wdfkd** 的输出示例。

```dbgcmd
0: kd> !wdfkd.wdfumirps
Number of pending IRPS: 0x4
####  CWudfIrp     Current Type           UniqueId KernelIrp         Device Stack
----  ----------------  --------------------------------------------------  ----
0000  1ab9e90c40   WdfRequestUndefined        0     0                 1ab9eaa6d0
0001  1ab9ebfa90   WdfRequestInternalIoctl    0     0                 1ab9eaa6d0
0002  1ab9ebfd10   WdfRequestInternalIoctl    0     0                 1ab9eaa6d0
0003  1ab9eae370   Power (WAIT_WAKE)          0     ffffe00000c53010  1ab9eaa6d0
```

 

 





