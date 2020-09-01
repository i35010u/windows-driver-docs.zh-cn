---
title: KSPROPERTY \_ 音频 \_ WAVERT \_ 当前 \_ 写入 \_ LASTBUFFER \_ 位置
description: KSPROPERTY \_ audio \_ WAVERT \_ CURRENT \_ WRITE \_ LASTBUFFER \_ POSITION 属性用于指示音频缓冲区中的最后一个有效字节。
ms.assetid: 01EC2F29-D30A-4017-841F-8443D7C4BCF6
keywords:
- KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2fe8162d2f2ed9b146d358cdd1cb1253bcb09a7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206929"
---
# <a name="ksproperty_audio_wavert_current_write_lastbuffer_position"></a>KSPROPERTY \_ 音频 \_ WAVERT \_ 当前 \_ 写入 \_ LASTBUFFER \_ 位置


KSPROPERTY \_ audio \_ WAVERT \_ CURRENT \_ WRITE \_ LASTBUFFER \_ POSITION 属性用于指示音频缓冲区中的最后一个有效字节。

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
<th align="left">获取</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>节点 via 引脚实例</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 ULONG，表示 WaveRT 音频缓冲区中的最后一个有效字节。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ AUDIO \_ WAVERT \_ CURRENT \_ WRITE \_ LASTBUFFER \_ POSITION 属性请求返回状态 \_ SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

如果客户端应用向 \_ \_ \_ \_ 音频驱动程序发送 KSPROPERTY 音频 WAVERT 当前写入 LASTBUFFER 位置属性请求时使用了 KSPROPERTY 类型 BASICSUPPORT 标志 \_ \_ \_ \_ ，并且返回了 "成功" 状态 \_ ，则它将确认该驱动程序支持新添加的 "KSPROPERTY \_ 音频 \_ WAVERT \_ 当前 \_ 写入 \_ LASTBUFFER \_ 位置" 属性。

当客户端应用程序对要由卸载的流的音频驱动程序处理的音频缓冲区执行最后一次写入操作时，音频驱动程序将调用 [**SetStreamCurrentWritePositionForLastBuffer**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportstreamaudioenginenode2-setstreamcurrentwritepositionforlastbuffer) 方法。 **SetStreamCurrentWritePositionForLastBuffer**方法指示流中最后一个缓冲区的 "写入位置"。 请注意，最后一个缓冲区只能部分填充。

如果开发的音频驱动程序不是为了与音频端口类驱动程序一起使用 (Portcls) ，则必须为此新的 KS 属性实现自己的属性处理程序。

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
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**SetStreamCurrentWritePositionForLastBuffer**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportstreamaudioenginenode2-setstreamcurrentwritepositionforlastbuffer)

 

