---
title: wdfkd.wdfsetdriver
description: Wdfkd.wdfsetdriver 扩展设置的调试器扩展命令将应用默认内核模式驱动程序框架 (KMDF) 驱动程序的名称。
ms.assetid: 90fc99a0-1e78-44bb-ba91-191f116160e7
keywords:
- wdfkd.wdfsetdriver Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfsetdriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1e7e5457c64ab31256a4b5b2a9dc4947b5f41b9c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554057"
---
# <a name="wdfkdwdfsetdriver"></a>!wdfkd.wdfsetdriver


**！ Wdfkd.wdfsetdriver**扩展设置到的调试器扩展命令将应用默认内核模式驱动程序框架 (KMDF) 驱动程序的名称。

```dbgcmd
!wdfkd.wdfsetdriver DriverName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *DriverName*   
驱动程序的名称。 *DriverName*不得包含.sys 文件扩展名。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

**！ Wdfkd.wdfsetdriver**扩展设置的默认驱动程序名称。 您可以使用此名称与其他**wdfkd**就不再需要你指定的驱动程序名称的扩展。

若要获取当前默认 KMDF 驱动程序的名称，请使用[ **！ wdfkd.wdfgetdriver** ](-wdfkd-wdfgetdriver.md)扩展。

 

 





