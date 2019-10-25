---
title: KSPROPERTY\_音频\_WAVERT\_当前\_写入\_LASTBUFFER\_位置
description: KSPROPERTY\_音频\_WAVERT\_当前\_WRITE\_LASTBUFFER\_POSITION 属性用于指示音频缓冲区中的最后一个有效字节。
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
ms.openlocfilehash: 078f02f46d898dcfc12d3a1a9a1742d3a2de27e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830928"
---
# <a name="ksproperty_audio_wavert_current_write_lastbuffer_position"></a>KSPROPERTY\_音频\_WAVERT\_当前\_写入\_LASTBUFFER\_位置


KSPROPERTY\_音频\_WAVERT\_当前\_WRITE\_LASTBUFFER\_POSITION 属性用于指示音频缓冲区中的最后一个有效字节。

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
<td align="left"><p>无</p></td>
<td align="left"><p>“是”</p></td>
<td align="left"><p>节点 via 引脚实例</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 ULONG，表示 WaveRT 音频缓冲区中的最后一个有效字节。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_WAVERT\_当前\_写入\_LASTBUFFER\_位置属性请求返回状态\_SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

如果客户端应用程序使用 KSPROPERTY\_请在\_BASICSUPPORT 标志发送 KSPROPERTY\_音频\_WAVERT\_当前\_写入\_LASTBUFFER\_位置属性请求发送到音频驱动程序和状态返回\_SUCCESS 后，它将确认驱动程序支持新添加的 KSPROPERTY\_音频\_WAVERT\_当前\_写入\_LASTBUFFER\_POSITION 属性。

当客户端应用程序对要由卸载的流的音频驱动程序处理的音频缓冲区执行最后一次写入操作时，音频驱动程序将调用[**SetStreamCurrentWritePositionForLastBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportstreamaudioenginenode2-setstreamcurrentwritepositionforlastbuffer)方法。 **SetStreamCurrentWritePositionForLastBuffer**方法指示流中最后一个缓冲区的 "写入位置"。 请注意，最后一个缓冲区只能部分填充。

如果开发的音频驱动程序未设计为与音频端口类驱动程序（Portcls）一起使用，则必须为此新的 KS 属性实现自己的属性处理程序。

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


[**SetStreamCurrentWritePositionForLastBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportstreamaudioenginenode2-setstreamcurrentwritepositionforlastbuffer)

 

 






