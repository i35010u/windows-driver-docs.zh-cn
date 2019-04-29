---
title: wdfkd.wdfumirps
description: Wdfkd.wdfumirps 扩展显示隐式的过程中挂起用户模式下 I/O 请求数据包 (UM Irp) 的列表。
ms.assetid: 1BFFDAC0-AA1F-434A-BB05-6864810F9B98
keywords:
- wdfkd.wdfumirps Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumirps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0ab52b2fcde71bd6d8a1c8ae4f24e0f1ff861d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323383"
---
# <a name="wdfkdwdfumirps"></a>!wdfkd.wdfumirps


**！ Wdfkd.wdfumirps**扩展中显示挂起的用户模式下 I/O 请求数据包 (UM Irp) 的列表[隐式过程](controlling-threads-and-processes.md)。

```dbgcmd
!wdfkd.wdfumirps NumberOfIrps Flags
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______NumberOfIrps______"></span><span id="_______numberofirps______"></span><span id="_______NUMBEROFIRPS______"></span> *NumberOfIrps*   
可选。 指定的挂起 UM Irp 以显示有关的信息的数目。 如果*NumberOfIrps*是一个星号 (\*) 或被省略，就会显示所有 UM Irp。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息的类型。 *标志*可以是以下位的任意组合。 默认值为 0x01。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>位 0 (0x01)  
显示有关挂起 Irp 的详细信息。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

在内核模式调试会话中或在用户模式下调试会话附加到 UMDF 主机进程 (wudfhost.exe)，可以使用此命令。

此命令显示相同的信息作为用户模式命令[ **！ wudfext.umirps**](-wudfext-umirps.md)。

可以使用[ **！ 过程**](-process.md)若要获取所有 UMDF 主机进程，，和一系列可以使用[ **.process** ](-process--set-process-context-.md)之一设置隐式的进程UMDF 主机进程。 有关详细示例，请参阅[ **！ wdfkd.wdfumdevstacks**](-wdfkd-wdfumdevstacks.md)。

下面是输出的示例 **！ wdfkd.wdfumirps**。

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

 

 





