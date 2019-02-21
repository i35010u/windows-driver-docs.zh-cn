---
title: WIA\_IPA\_MIN\_缓冲区\_大小
description: WIA\_IPA\_MIN\_缓冲区\_大小属性指定数据传输中使用的最小缓冲区大小。
ms.assetid: 0d289645-666c-4b67-8971-cdeff3caef3e
keywords:
- WIA_IPA_MIN_BUFFER_SIZE 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_MIN_BUFFER_SIZE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a038ca873179974a9d2f4958bc3d129fce867c0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541446"
---
# <a name="wiaipaminbuffersize"></a>WIA\_IPA\_MIN\_缓冲区\_大小


WIA\_IPA\_MIN\_缓冲区\_大小属性指定数据传输中使用的最小缓冲区大小。

## <span id="ddk_wia_ipa_min_buffer_size_si"></span><span id="DDK_WIA_IPA_MIN_BUFFER_SIZE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

如果通过一种回调机制，WIA 执行数据传输\_IPA\_MIN\_缓冲区\_大小属性值可以为最小可为 64 KB。 但是，如果传输文件，该属性值是所需一次传输一页数据的字节数。 WIA 微型驱动程序创建并维护此 WIA 属性。

WIA\_IPA\_MIN\_缓冲区\_大小等同于[ **WIA\_IPA\_缓冲区\_大小**](wia-ipa-buffer-size.md)属性。

应用程序可以读取 WIA\_IPA\_MIN\_缓冲区\_大小，以确定驱动程序指定的缓冲区大小的数据传输。 WIA 服务还会读取此属性，以便在数据传输的过程为微型驱动程序分配内存。

**请注意**  值的 WIA\_IPA\_MIN\_缓冲区\_大小属性包含为最小的应用程序可以请求在任何给定时间的数据量。 缓冲区大小越大，将会越大将请求发送到设备。 此较大的缓冲区大小可以使该设备出现缓慢甚至失去反应、 可能会降低总体计算机性能，以及可能会消耗过多资源。 缓冲区大小太小而降低性能的数据传输需要多个较小的请求。 通过考虑到你的设备、 请求数和这些请求的大小的数据请求的典型大小选择合理的缓冲区大小。

 

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
<td><p>对于 Windows Vista 驱动程序的所有传输启用项可选。 如果实施此属性，则编写的 Windows Server 2003、 Windows XP 和早期 Windows 版本的应用程序可以估计的传输缓冲区大小，并将因此，最佳的传输速率。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_IPA\_缓冲区\_大小**](wia-ipa-buffer-size.md)

 

 






