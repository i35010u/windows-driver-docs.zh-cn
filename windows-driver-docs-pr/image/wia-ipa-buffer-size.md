---
title: WIA\_IPA\_缓冲区\_大小
description: WIA\_IPA\_缓冲区\_大小属性包含缓冲区的大小，以字节为单位，在数据传输过程中使用。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 2feb26fa-674d-4dc2-b8bb-51942cb48737
keywords:
- WIA_IPA_BUFFER_SIZE 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_BUFFER_SIZE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e7b26b1ecbfaf9266b2b593ae6343371f6470c4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369561"
---
# <a name="wiaipabuffersize"></a>WIA\_IPA\_缓冲区\_大小


WIA\_IPA\_缓冲区\_大小属性包含缓冲区的大小，以字节为单位，在数据传输过程中使用。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_buffer_size_si"></span><span id="DDK_WIA_IPA_BUFFER_SIZE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

WIA\_IPA\_缓冲区\_SIZE 属性等同于[ **WIA\_IPA\_MIN\_缓冲区\_大小**](wia-ipa-min-buffer-size.md)属性。

应用程序可以读取 WIA\_IPA\_缓冲区\_大小，以确定驱动程序指定的缓冲区大小的数据传输。 WIA 服务还会读取此属性，以便在数据传输的过程为微型驱动程序分配内存。

**请注意**  值的 WIA\_IPA\_缓冲区\_大小属性包含为最小的应用程序可以请求在任何给定时间的数据量。 缓冲区大小越大，将会越大将请求发送到设备。 此较大的缓冲区大小可以使设备看起来缓慢甚至失去反应，可能会降低总体计算机性能，并可能会消耗过多资源。 缓冲区大小太小而降低性能的数据传输需要多个较小的请求。 通过考虑到你的设备、 请求数和这些请求的大小的数据请求的典型大小选择合理的缓冲区大小。

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>对于 Windows Vista 驱动程序的所有传输启用项可选。 如果实现此属性，专为 Windows Server 2003、 Windows XP 和早期版本的 Windows 的应用程序可以估计的传输缓冲区大小，并且，因此，是最佳的传输速率。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPA\_MIN\_缓冲区\_大小**](wia-ipa-min-buffer-size.md)

 

 






