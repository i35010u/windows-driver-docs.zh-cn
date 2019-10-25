---
title: KSPROPERTY\_AEC\_模式
description: KSPROPERTY\_AEC\_模式属性用于控制 AEC 节点的操作模式。 这是 AEC 节点的一个可选属性（KSNODETYPE\_声音\_回音\_"取消"）。
ms.assetid: 79f0d655-4764-454f-8867-6cf1b5cedc82
keywords:
- KSPROPERTY_AEC_MODE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AEC_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d7cb680fc14c3dde6f4f9692b240f659cb72a10
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831138"
---
# <a name="ksproperty_aec_mode"></a>KSPROPERTY\_AEC\_模式


KSPROPERTY\_AEC\_模式属性用于控制 AEC 节点的操作模式。 这是 AEC 节点的一个可选属性（[**KSNODETYPE\_声音\_回音\_"取消**](ksnodetype-acoustic-echo-cancel.md)"）。

## <span id="ddk_ksproperty_aec_mode_ks"></span><span id="DDK_KSPROPERTY_AEC_MODE_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>“是”</p></td>
<td align="left"><p>大头针</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 ULONG，可以设置为标头文件 Ksmedia 中的以下模式常量之一：

-   AEC\_模式\_通过\_

    在直通模式下，AEC 节点允许捕获和呈现数据，以便在不进行修改的情况下直接传递节点。

-   AEC\_模式\_半\_双工

    AEC 算法在半双工模式下运行，该模式在操作中与播音电话类似。 在此模式下，每当本地人物的语音具有比远程人员更高的音量级别时，扬声器音量就会静音。

-   AEC\_模式\_FULL\_双工

    AEC 算法在全双工模式下运行。

传递模式为默认值。 当创建包含 AEC 节点的筛选器或重置节点时，该节点最初配置为在传递模式下运行。

在 Windows XP 的初始版本中， [aec 系统筛选器](https://docs.microsoft.com/windows-hardware/drivers/audio/aec-system-filter)使用的 aec 算法不支持半双工模式。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AEC\_模式属性请求返回状态\_SUCCESS，以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_声音\_回音\_取消**](ksnodetype-acoustic-echo-cancel.md)

 

 






