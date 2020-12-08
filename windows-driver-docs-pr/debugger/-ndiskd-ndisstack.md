---
title: ndiskd.ndisstack
description: ！ Ndiskd ndisstack 扩展显示调试堆栈跟踪。
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
ms.openlocfilehash: fe3eeaddf0849253e7f43ff49cf52fa9e0bcfe46
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805813"
---
# <a name="ndiskdndisstack"></a>!ndiskd.ndisstack


**注意**  第三方网络驱动程序开发人员不需要手动使用此扩展命令。 您可以运行它来查看它所显示的信息，但不能重复使用它在您的驱动程序中提供的详细信息。

 

**！ Ndiskd ndisstack** 扩展显示调试堆栈跟踪。

```console
!ndiskd.ndisstack -handle <x> [-statistics]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
必需。 堆栈块的句柄。

<span id="_______-statistics______"></span><span id="_______-STATISTICS______"></span>*-statistics*   
显示调试统计信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd.dll

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

 

