---
title: ks.automation
description: Ks.automation 扩展显示任何与给定对象关联的自动化项目。
ms.assetid: a8fd790f-2793-4e6e-a500-f61646be2c89
keywords:
- ks.automation Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.automation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f8a029c41e9f8c352ae6372d747580938837d96
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336330"
---
# <a name="ksautomation"></a>!ks.automation


**！ Ks.automation**扩展插件都会显示与给定对象关联的任何自动化项。

```dbgcmd
!ks.automation Object
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *Object*   
指定指向要为其显示自动化项对象的指针。 （自动化项是属性、 方法和事件）。*对象*必须是以下类型之一：PKSPIN，PKSFILTER，CKsPin\*，CKsFilter\*，PIRP。 如果*对象*是指向自动化 IRP，命令返回属性信息和处理程序。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[流式处理的内核调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

您可以使用此命令使用筛选器地址从获取[ **！ ks.enumdevobj**](-ks-enumdevobj.md)。

下面是举例 **！ ks.automation**显示。 参数是筛选器的地址：

```dbgcmd
kd> !automation 829493c4
Filter 829493c4 has the following automation items:
    Property Items:
        Set KSPROPSETID_Pin
            Item ID = KSPROPERTY_PIN_CINSTANCES
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000008
            Item ID = KSPROPERTY_PIN_CTYPES
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000018
                MinData = 00000004
            Item ID = KSPROPERTY_PIN_DATAFLOW
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000004
            Item ID = KSPROPERTY_PIN_DATARANGES
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000000
            Item ID = KSPROPERTY_PIN_DATAINTERSECTION
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000028
                MinData = 00000000
            Item ID = KSPROPERTY_PIN_INTERFACES
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000000
            Item ID = KSPROPERTY_PIN_MEDIUMS
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000000
            Item ID = KSPROPERTY_PIN_COMMUNICATION
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000004
            Item ID = KSPROPERTY_PIN_NECESSARYINSTANCES
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000004
            Item ID = KSPROPERTY_PIN_CATEGORY
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000010
            Item ID = KSPROPERTY_PIN_NAME
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000000
        Set KSPROPSETID_Topology
            Item ID = KSPROPERTY_TOPOLOGY_CATEGORIES
                Get Handler = ks!CKsFilter::Property_Topology
                Set Handler = NULL
                MinProperty = 00000018
                MinData = 00000000
            Item ID = KSPROPERTY_TOPOLOGY_NODES
                Get Handler = ks!CKsFilter::Property_Topology
                Set Handler = NULL
                MinProperty = 00000018
                MinData = 00000000
            Item ID = KSPROPERTY_TOPOLOGY_CONNECTIONS
                Get Handler = ks!CKsFilter::Property_Topology
                Set Handler = NULL
                MinProperty = 00000018
                MinData = 00000000
            Item ID = KSPROPERTY_TOPOLOGY_NAME
                Get Handler = ks!CKsFilter::Property_Topology
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000000
        Set KSPROPSETID_General
            Item ID = KSPROPERTY_GENERAL_COMPONENTID
                Get Handler = ks!CKsFilter::Property_General_ComponentId
                Set Handler = NULL
                MinProperty = 00000018
                MinData = 00000048
        Set [ks!KSPROPSETID_Frame]  a60d8368-5324-4893-b020-c431a50bcbe3
            Item ID = 0
                Get Handler = ks!CKsFilter::Property_Frame_Holding
                Set Handler = ks!CKsFilter::Property_Frame_Holding
                MinProperty = 00000018
                MinData = 00000004
    Method Items:
        NO SETS FOUND!
    Event Items:
        NO SETS FOUND!
```

 

 





