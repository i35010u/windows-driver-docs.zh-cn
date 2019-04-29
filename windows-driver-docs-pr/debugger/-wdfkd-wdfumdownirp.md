---
title: wdfkd.wdfumdownirp
description: Wdfkd.wdfumdownirp 扩展插件都会显示与指定的用户模式 IRP 相关联的内核模式 I/O 请求数据包 (IRP)。
ms.assetid: 98DFF193-950A-46CF-875E-B2907743F5D4
keywords:
- wdfkd.wdfumdownirp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumdownirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fee9988cb58e9e49f833d7f727286478823fc977
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323156"
---
# <a name="wdfkdwdfumdownirp"></a>!wdfkd.wdfumdownirp


**！ Wdfkd.wdfumdownirp**扩展插件都会显示与指定的用户模式 IRP 相关联的内核模式 I/O 请求数据包 (IRP)。 在两个步骤中使用此命令。 请参阅备注。

```dbgcmd
!wdfkd.wdfumdownirp UmIrp [FileObject] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______UmIrp______"></span><span id="_______umirp______"></span><span id="_______UMIRP______"></span> *UmIrp*   
指定的用户模式下 IRP 的地址。 可以使用[ **！ wdfkd.wdfumirps** ](-wdfkd-wdfumirps.md)以获取 UM Irp 中的地址[隐式过程](controlling-threads-and-processes.md)。

<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span> *FileObject*   
指定的地址**\_文件\_对象**结构。 有关如何获取此地址的信息，请参阅备注。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

在内核模式调试会话中或在用户模式下调试会话附加到 UMDF 主机进程 (wudfhost.exe)，可以使用此命令。

若要使用此命令，请执行以下步骤：

1.  请输入以下命令，将仅地址传递用户模式下 IRP。 该命令将显示一个句柄。
2.  传递显示的句柄[ **！ 处理**](-handle.md)命令。 中的输出 **！ 处理**，找到的地址**\_文件\_对象**结构。
3.  输入以下命令，将传递用户模式下 IRP 的地址和地址都**\_文件\_对象**结构。

 

 





