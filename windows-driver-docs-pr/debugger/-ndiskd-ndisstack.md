---
title: ndiskd.ndisstack
description: ！ Ndiskd.ndisstack 扩展显示调试堆栈跟踪。
ms.assetid: 939DEC34-3D20-41FE-B5A8-DDF810195B07
keywords:
- ndiskd.ndisstack Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2cd8e01ffc3d97669b132daa691931970e8f7b43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543079"
---
# <a name="ndiskdndisstack"></a>!ndiskd.ndisstack


**请注意**  第三方网络驱动程序开发人员不应手动使用此扩展命令。 你可以运行它以查看其显示的信息，但不能重复使用它提供了您的驱动程序的详细信息。

 

**！ Ndiskd.ndisstack**扩展显示调试堆栈跟踪。

```console
!ndiskd.ndisstack [-handle <x>] [-statistics] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 堆栈块的句柄。

<span id="_______-statistics______"></span><span id="_______-STATISTICS______"></span> *-statistics*   
显示了调试的统计信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

 

 






