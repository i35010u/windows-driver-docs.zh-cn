---
title: WIA\_IPA\_ITEM\_SIZE
description: WIA\_IPA\_项\_大小属性包含当前大小 （字节） 与 WIA 项相关联的数据。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: af019c00-715b-43d1-ba14-f20c01871f35
keywords:
- WIA_IPA_ITEM_SIZE 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_ITEM_SIZE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75ab1f9bebde852b4f2915e32ceff093170e6f9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388782"
---
# <a name="wiaipaitemsize"></a>WIA\_IPA\_ITEM\_SIZE


WIA\_IPA\_项\_大小属性包含当前大小 （字节） 与 WIA 项相关联的数据。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_item_size_si"></span><span id="DDK_WIA_IPA_ITEM_SIZE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

值的 WIA\_IPA\_项\_大小属性包含是要传输的数据的总大小。 如果此值为零，WIA 微型驱动程序具有数据的精确大小所需信息。 （这种情况下很常见的压缩数据。）

应用程序读取 WIA\_IPA\_项\_大小，以传输之前确定数据的大小。 WIA 服务读取此属性，以帮助中的数据传输分配内存。 有关数据传输的详细信息，请参阅[WIA 应用程序传输数据](https://msdn.microsoft.com/library/windows/hardware/ff548473)。

如果 WIA\_IPA\_项\_大小设置为零并且 TYMED 配置用于文件传输，WIA 服务不会为 WIA 微型驱动程序分配任何内存。

**请注意**  在 Windows Vista 和更高版本的操作系统仅设置 WIA\_IPA\_项\_大小属性设为 0 时启用自动文档大小检测的 ADF 项。

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





