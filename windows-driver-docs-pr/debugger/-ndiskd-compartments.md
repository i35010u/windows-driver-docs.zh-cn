---
title: ndiskd
description: Ndiskd 扩展显示所有网络隔离舱。
keywords:
- ndiskd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.compartments
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dd512463356f4a91fec8c58a23a56e8a87e43476
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832037"
---
# <a name="ndiskdcompartments"></a>!ndiskd.compartments


**！ Ndiskd** 扩展显示所有网络隔离舱。

```console
!ndiskd.compartments 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


此扩展没有参数。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd.dll

<a name="remarks"></a>备注
-------

通过隔离舱，NDIS 可以管理接口。 第三方接口提供程序仅使用主隔离舱，如 [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的 **CompartmentId** 成员中所述。

<a name="examples"></a>示例
--------

运行 **！ ndiskd** 扩展，查看所有网络隔离舱的列表。 在此示例中，只有一个隔离舱 (主) 。

```console
3: kd> !ndiskd.compartments
    Compartment        ffffdf80139b9940
    ID                 1
    Loopback Network   ffffdf80139b8900
    Loopback Interface ffffdf80139b6a20
    Networks:
                       ffffdf80139b8900    [Unnamed network]
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

 

