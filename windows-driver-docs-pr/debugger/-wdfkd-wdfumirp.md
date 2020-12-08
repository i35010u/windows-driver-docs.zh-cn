---
title: wdfkd.wdfumirp
description: Wdfkd wdfumirp 扩展显示有关用户模式 i/o 请求包 (UM IRP) 的信息。
keywords:
- wdfkd wdfumirp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 983c8c6826f087319cd359faf3be1ece605b7d6b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823623"
---
# <a name="wdfkdwdfumirp"></a>!wdfkd.wdfumirp


**！ Wdfkd wdfumirp** 扩展显示有关用户模式 i/o 请求数据包 (UM IRP) 的信息。

```dbgcmd
!wdfkd.wdfumirp Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示其相关信息的 UM IRP 的地址。 可以使用！ wdfumirps 获取 [隐式进程](controlling-threads-and-processes.md)中 UM irp 的地址 [**wdfkd。**](-wdfkd-wdfumirps.md)

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作


UMDF 2

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

可以在内核模式调试会话中或在附加到 UMDF 主机进程 ( # A0) 的用户模式调试会话中使用此命令。

此命令显示与用户模式命令 [**！ wudfext**](-wudfext-umirp.md)相同的信息。

您可以使用 [**！进程**](-process.md) 获取所有 umdf 主机进程的列表，并且可以使用 [**. 进程**](-process--set-process-context-.md) 将隐式进程设置为一个 umdf 主机进程。 有关详细示例，请参阅 [**！ wdfkd. wdfumdevstacks**](-wdfkd-wdfumdevstacks.md)。

下面演示了如何使用 [**！ wdfkd**](-wdfkd-wdfumirps.md) 和 **！ wdfkd** 显示有关单个 UM IRP 的信息。

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

 

 





