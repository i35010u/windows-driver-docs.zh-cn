---
title: ndiskd.compartments
description: Ndiskd.compartments 扩展显示所有的网络隔离舱。
ms.assetid: F9BF319D-77E9-4D12-84E9-655058F57AC4
keywords:
- ndiskd.compartments Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.compartments
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 77959db759c5ca646c5d58f0a234806fc3294b5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336000"
---
# <a name="ndiskdcompartments"></a>!ndiskd.compartments


**！ Ndiskd.compartments**扩展插件都会显示所有的网络隔离舱。

```console
!ndiskd.compartments 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


此扩展没有任何参数。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="remarks"></a>备注
-------

隔离舱是 NDIS 管理接口的方法。 第三方接口提供程序仅使用主隔离舱，如中所述**CompartmentId**的成员[ **NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)结构。

<a name="examples"></a>示例
--------

运行 **！ ndiskd.compartments**扩展以查看所有的网络隔离舱的列表。 在此示例中，没有只有一个隔离舱 （主一个）。

```console
3: kd> !ndiskd.compartments
    Compartment        ffffdf80139b9940
    ID                 1
    Loopback Network   ffffdf80139b8900
    Loopback Interface ffffdf80139b6a20
    Networks:
                       ffffdf80139b8900    [Unnamed network]
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NDIS\_BIND\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff564832)

 

 






