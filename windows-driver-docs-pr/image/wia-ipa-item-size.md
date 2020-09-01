---
title: WIA \_ IPA \_ 项 \_ 大小
description: WIA \_ IPA \_ ITEM \_ SIZE 属性包含与 WIA 项关联的数据的当前大小（以字节为单位）。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: af019c00-715b-43d1-ba14-f20c01871f35
keywords:
- WIA_IPA_ITEM_SIZE 图像设备
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
ms.openlocfilehash: 5d2ef6e77cec2c149226d7a5bcd8b0c3f5feba55
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193245"
---
# <a name="wia_ipa_item_size"></a>WIA \_ IPA \_ 项 \_ 大小


WIA \_ IPA \_ ITEM \_ SIZE 属性包含与 WIA 项关联的数据的当前大小（以字节为单位）。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_item_size_si"></span><span id="DDK_WIA_IPA_ITEM_SIZE_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>注解
-------

WIA \_ IPA \_ ITEM \_ SIZE 属性包含的值是正在传输的数据的总大小。 如果此值为零，则 WIA 微型驱动程序不包含有关数据的准确大小的信息。  (这种情况通常适用于压缩的数据。 ) 

应用程序 \_ \_ 在传输数据之前，读取 WIA IPA 项 \_ 大小以确定数据的大小。 WIA 服务读取此属性，以帮助分配用于数据传输的内存。 有关数据传输的详细信息，请参阅 [将数据传输到 WIA 应用程序](./transferring-data-to-a-wia-application.md)。

如果 WIA \_ IPA \_ ITEM \_ SIZE 设置为0，并且为文件传输配置 TYMED，wia 服务不会为 wia 微型驱动程序分配任何内存。

**注意**   在 Windows Vista 和更高版本的操作系统中， \_ \_ \_ 当启用自动文档大小检测功能时，仅将 ADF 项的 "WIA IPA item SIZE" 属性设置为0。

 

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
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

