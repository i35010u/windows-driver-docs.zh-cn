---
title: wdfkd.wdfumirp
description: Wdfkd.wdfumirp 扩展显示有关用户模式下 I/O 请求数据包 (UM IRP) 的信息。
ms.assetid: 8706E8F6-A387-48A9-AF14-ED2C0F94AD98
keywords:
- wdfkd.wdfumirp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 39c9546381135db9ecd25c765062e5177896d71d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323150"
---
# <a name="wdfkdwdfumirp"></a>!wdfkd.wdfumirp


**！ Wdfkd.wdfumirp**扩展显示有关用户模式下 I/O 请求数据包 (UM IRP) 的信息。

```dbgcmd
!wdfkd.wdfumirp Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的地址 UM IRP 以显示有关的信息。 可以使用[ **！ wdfkd.wdfumirps** ](-wdfkd-wdfumirps.md)以获取 UM Irp 中的地址[隐式过程](controlling-threads-and-processes.md)。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

在内核模式调试会话中或在用户模式下调试会话附加到 UMDF 主机进程 (wudfhost.exe)，可以使用此命令。

此命令显示相同的信息作为用户模式命令[ **！ wudfext.umirp**](-wudfext-umirp.md)。

可以使用[ **！ 过程**](-process.md)若要获取所有 UMDF 主机进程，，和一系列可以使用[ **.process** ](-process--set-process-context-.md)之一设置隐式的进程UMDF 主机进程。 有关详细示例，请参阅[ **！ wdfkd.wdfumdevstacks**](-wdfkd-wdfumdevstacks.md)。

以下示例演示如何使用[ **！ wdfkd.wdfumirps** ](-wdfkd-wdfumirps.md)并 **！ wdfkd.wdfumirp**来显示单独的 UM IRP 有关的信息。

```dbgcmd
0: kd> !wdfkd.wdfumirps
Number of pending IRPS: 0x4
####  CWudfIrp     Current Type           UniqueId KernelIrp         Device Stack
----  ----------------  --------------------------------------------------  ----
...
0003  1ab9eae370   Power (WAIT_WAKE)          0     ffffe00000c53010  1ab9eaa6d0

0: kd> !wdfkd.wdfumirp 1ab9eae370
UM IRP: 0x0000001ab9eae370  UniqueId: 0x0  Kernel Irp: 0xffffe00000c53010
  Type: Power (WAIT_WAKE)
  ClientProcessId: 0x0
  Device Stack: 0x0000001ab9eaa6d0
  IoStatus
    hrStatus: 0x0
    Information: 0x0
  Total number of stack locations: 2
  CurrentStackLocation: StackLocation[ 0 ]
  > StackLocation[ 0 ]
      FxDevice:   (None)
      Completion:
        Callback:   0x0000000000000000
        Context:    0x0000001ab9ebc750
    StackLocation[ 1 ]
    ...
```

 

 





