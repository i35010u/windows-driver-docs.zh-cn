---
title: wdfkd.wdfumfile
description: Wdfkd.wdfumfile 扩展显示有关 UMDF 内部堆栈文件的信息。
ms.assetid: AAE9E003-829D-4A52-8F67-58DFE15D5D3C
keywords:
- wdfkd.wdfumfile Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumfile
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d20f4369ef1a3cb5fdf21db7ad432ee263fb7ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544872"
---
# <a name="wdfkdwdfumfile"></a>!wdfkd.wdfumfile


**！ Wdfkd.wdfumfile**扩展显示 UMDF 内部堆栈文件有关的信息。

```dbgcmd
!wdfkd.wdfumfile Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示有关的信息的 UMDF 内部堆栈文件的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

在内核模式调试会话中或在用户模式下调试会话附加到 UMDF 主机进程 (wudfhost.exe)，可以使用此命令。

此命令显示相同的信息作为用户模式命令[ **！ wudfext.umfile**](-wudfext-umfile.md)。

 

 





