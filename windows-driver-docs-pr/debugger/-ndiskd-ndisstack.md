---
title: ndiskd.ndisstack
description: ！ Ndiskd ndisstack 扩展显示调试堆栈跟踪。
ms.assetid: 939DEC34-3D20-41FE-B5A8-DDF810195B07
keywords:
- ndiskd ndisstack Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 00e6ffb04f3c6420e59f3f26e938817d788483de
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837580"
---
# <a name="ndiskdndisstack"></a>!ndiskd.ndisstack


**请注意**  第三方网络驱动程序开发人员不需要手动使用此扩展命令。 您可以运行它来查看它所显示的信息，但不能重复使用它在您的驱动程序中提供的详细信息。

 

**！ Ndiskd ndisstack**扩展显示调试堆栈跟踪。

```console
!ndiskd.ndisstack [-handle <x>] [-statistics] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 堆栈块的句柄。

<span id="_______-statistics______"></span><span id="_______-STATISTICS______"></span> *-statistics*   
显示调试统计信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展（Ndiskd）** ](ndis-extensions--ndiskd-dll-.md)

[ **！ ndiskd。帮助**](-ndiskd-help.md)

 

 






