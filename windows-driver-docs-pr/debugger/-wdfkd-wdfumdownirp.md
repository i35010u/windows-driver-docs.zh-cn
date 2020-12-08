---
title: wdfkd.wdfumdownirp
description: Wdfumdownirp 扩展显示与指定的用户模式 IRP 关联 (IRP) 的内核模式 i/o 请求包。
keywords:
- wdfkd wdfumdownirp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumdownirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aab1b496822abaea0cdf4c00b991de7bf2b7e6c4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823627"
---
# <a name="wdfkdwdfumdownirp"></a>!wdfkd.wdfumdownirp


**！ Wdfkd wdfumdownirp** 扩展显示与指定的用户模式 IRP 关联的内核模式 i/o 请求数据包 (IRP) 。 在两个步骤中使用此命令。 请参阅“备注”。

```dbgcmd
!wdfkd.wdfumdownirp UmIrp [FileObject] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______UmIrp______"></span><span id="_______umirp______"></span><span id="_______UMIRP______"></span>*UmIrp*   
指定用户模式 IRP 的地址。 可以使用！ wdfumirps 获取 [隐式进程](controlling-threads-and-processes.md)中 UM irp 的地址 [**wdfkd。**](-wdfkd-wdfumirps.md)

<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span>*FileObject*   
指定 **\_ 文件 \_ 对象** 结构的地址。 有关如何获取此地址的信息，请参阅 "备注"。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作


UMDF 2

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

可以在内核模式调试会话中或在附加到 UMDF 主机进程 ( # A0) 的用户模式调试会话中使用此命令。

若要使用此命令，请执行以下步骤：

1.  输入此命令，只传递用户模式 IRP 的地址。 该命令显示一个句柄。
2.  将显示的句柄传递给 [**！ handle**](-handle.md) 命令。 在 **！句柄** 的输出中，找到 **\_ 文件 \_ 对象** 结构的地址。
3.  再次输入此命令，同时传递用户模式 IRP 的地址和 **\_ 文件 \_ 对象** 结构的地址。

 

 





