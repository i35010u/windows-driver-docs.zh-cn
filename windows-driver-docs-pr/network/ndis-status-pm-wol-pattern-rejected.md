---
title: NDIS_STATUS_PM_WOL_PATTERN_REJECTED
description: NDIS_STATUS_PM_WOL_PATTERN_REJECTED 状态指示过量电源管理唤醒 LAN 唤醒 (WOL) 模式已被拒绝的驱动程序。
ms.assetid: 49180c69-a3b8-4a6f-b34f-93e063c88f43
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PM_WOL_PATTERN_REJECTED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2e1448707fc13435ea58e8e7c0fbeef8a645def9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523516"
---
# <a name="ndisstatuspmwolpatternrejected"></a>NDIS\_状态\_PM\_WOL\_模式\_已拒绝


NDIS\_状态\_PM\_WOL\_模式\_已拒绝状态指示为过量电源管理唤醒 LAN 唤醒 (WOL) 模式已被拒绝的驱动程序。

<a name="remarks"></a>备注
-------

NDIS 或微型端口驱动程序可以生成 NDIS\_状态\_PM\_WOL\_模式\_已拒绝状态指示当其中任一个删除 WOL 模式时。 **StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构包含的 WOL 模式标识符的 ULONG拒绝 WOL 模式。 NDIS 提供中的 WOL 模式标识符**PatternId**的成员[ **NDIS\_PM\_WOL\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566768)结构。

NDIS 生成 NDIS\_状态\_PM\_WOL\_模式\_已拒绝状态指示它必须从网络适配器中删除以前添加的 WOL 模式。 例如，NDIS 可能会删除以释放资源的更高的优先级 WOL 模式的 WOL 模式。 添加已删除的模式的绑定将只发送通知事件。

对于使用基础结构元素来卸载模式以及在基础结构间漫游的无线网络适配器，就可以新基础结构元素可能不支持与前一个相同的功能。 在这种情况下，微型端口驱动程序可以向 NDIS，发出的状态指示，NDIS 将会发布 NDIS\_状态\_PM\_WOL\_模式\_拒绝特定错误代码。

WiFi 驱动程序可能会缓存本地唤醒模式。 当驱动程序用于添加或删除唤醒模式处理 OID 时，该驱动程序可以选择仅更新其本地缓存。 该驱动程序可以延迟的基础结构更新，直到收到[OID\_PM\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569768)OID。

基础结构可能没有足够的资源来满足所有唤醒模式。 在这种情况下，基础结构可以接受唤醒模式的部分列表。 微型端口驱动程序完成 OID\_PM\_参数设置请求，该驱动程序必须进行 NDIS\_状态\_PM\_WOL\_模式\_已拒绝状态为每个访问点 (AP) 拒绝的 WOL 模式的迹象。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>支持 NDIS 6.20 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_PM\_WOL\_PATTERN**](https://msdn.microsoft.com/library/windows/hardware/ff566768)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_PM\_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff569768)

 

 




