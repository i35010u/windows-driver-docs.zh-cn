---
title: KSPROPERTY\_JACK\_CONTAINERID
description: KSPROPERTY\_JACK\_CONTAINERID 属性实现为一个 pin-wise 属性，可通过使用筛选器句柄。
ms.assetid: 01A157B0-41EE-4713-B5D3-B9BF9C2B80CE
keywords:
- KSPROPERTY_JACK_CONTAINERID 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK_CONTAINERID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70f69ce0942f55f617ec6ee7b83f752e418fc86a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332707"
---
# <a name="kspropertyjackcontainerid"></a>KSPROPERTY\_JACK\_CONTAINERID


KSPROPERTY\_JACK\_CONTAINERID 属性实现为一个 pin-wise 属性，可通过使用筛选器句柄。

可以在任何与一个或多个物理插孔或其他有线或无线连接相关联的桥插针上支持此属性。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>（通过筛选器句柄） 的 pin 工厂</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td align="left"><p><strong>GUID</strong></p></td>
</tr>
</tbody>
</table>

 

属性值 （实例数据） 是一个 GUID。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_JACK\_CONTAINERID 属性请求返回具有与物理插孔或其他有线或无线连接相关联的设备的容器 ID 的 GUID。

<a name="remarks"></a>备注
-------

音频驱动程序应支持此属性，当且仅当满足以下条件：

-   关联的音频设备的容器 ID 是不同于为其加载音频驱动程序的设备节点的容器 ID。

-   该驱动程序可以获得通过其他方式的正确的容器 ID。

KSPROPERTY\_JACK\_CONTAINERID 属性只需从音频适配器质塑料制成的另一个音频终结点是否填充。 默认情况下的音频的终结点将继承其父容器 ID。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**BTHHFP\_描述符**](https://msdn.microsoft.com/library/windows/hardware/dn302030)

[**IOCTL\_BTHHFP\_设备\_获取\_CONTAINERID**](https://msdn.microsoft.com/library/windows/hardware/dn265107)

 

 






