---
title: 映射具有相同 ID 和名称的 WIA 属性
description: 映射具有相同 ID 和名称的 WIA 属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a892cba84746fdf82fa6e6351f4332e2c49af179
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816237"
---
# <a name="mapping-wia-properties-with-the-same-ids-and-names"></a>映射具有相同 ID 和名称的 WIA 属性


存在与 Windows Vista 对应项具有相同属性 Id 和属性名称的 Windows XP 属性。 下面是在 Windows Vista 中将其转换为的 Windows XP 根属性和平板和进纸器 (ADF) 属性的表格。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Windows XP 属性</strong></p></td>
<td><p><strong>Windows XP</strong></p>
<p><strong>项/上下文</strong></p></td>
<td><p><strong>Windows Vista 属性</strong></p></td>
<td><p><strong>Windows Vista 项</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_NAME</p>
<p>只读访问，请参阅备注： d</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
<td><p>WIA_IPA_ITEM_NAME</p>
<p>只读访问，请参阅备注： d</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ITEM_NAME</p>
<p>或泛型： "平板"</p>
<p>只读访问，请参阅注释： d 和 e</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ITEM_NAME</p>
<p>只读访问，请参阅注释： d 和 e</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_NAME</p>
<p>或泛型： "输送器"</p>
<p>只读访问，请参阅注释： d 和 e</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_ITEM_NAME</p>
<p>只读访问，请参阅注释： d 和 e</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>只读访问，请参阅备注： d</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>只读访问，请参阅备注： d</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>或泛型： "\Root\FLATBED"</p>
<p>只读访问，请参阅注释： d 和 e</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>或泛型： "\Root\FEEDER"</p>
<p>只读访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>只读访问，请参阅注释： d 和 e</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_TIME</p>
<p>只读访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ITEM_TIME</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ITEM_TIME</p>
<p>只读访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_ITEM_TIME</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>只读访问，请参阅注释： d 和 e</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>只读访问，请参阅注释： d 和 e</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>只读访问，请参阅注释： d 和 e</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>只读访问，请参阅注释： d 和 e</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>只读访问，请参阅注释： d 和 e</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>只读访问，请参阅注释： d 和 e</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>只读访问</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>只读访问</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>只读访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>只读访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_DATATYPE</p>
<p>请参阅备注： b</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_DATATYPE</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_DATATYPE</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_DATATYPE</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_DEPTH</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_DEPTH</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_DEPTH</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_DEPTH</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_PREFERRED_FORMAT</p>
<p>只读访问，请参阅备注： f</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_PREFERRED_FORMAT</p>
<p>只读访问，请参阅备注： f</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_PREFERRED_FORMAT</p>
<p>只读访问，请参阅备注： f</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_PREFERRED_FORMAT</p>
<p>只读访问，请参阅备注： f</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_FORMAT</p>
<p>读/写访问权限，请参阅说明： h 和 i</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_FORMAT</p>
<p>读/写访问权限，请参阅说明： h 和 i</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_FORMAT</p>
<p>读/写访问权限，请参阅说明： h 和 i</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_FORMAT</p>
<p>读/写访问权限，请参阅说明： h 和 i</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_COMPRESSION</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_COMPRESSION</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_COMPRESSION</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_COMPRESSION</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_TYMED</p>
<p>读/写访问权限，请参阅说明： h、i 和 k</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_TYMED</p>
<p>读/写访问权限，请参阅说明： h、i 和 k</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_TYMED</p>
<p>读/写访问权限，请参阅说明： h 和 i</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_TYMED</p>
<p>读/写访问权限，请参阅说明： h 和 i</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_CHANNELS_PER_PIXEL</p>
<p>只读访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_CHANNELS_PER_PIXEL</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_CHANNELS_PER_PIXEL</p>
<p>只读访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_CHANNELS_PER_PIXEL</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_BITS_PER_CHANNEL</p>
<p>只读访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_BITS_PER_CHANNEL</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_BITS_PER_CHANNEL</p>
<p>只读访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_BITS_PER_CHANNEL</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_SIZE</p>
<p>只读访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ITEM_SIZE</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ITEM_SIZE</p>
<p>只读访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_ITEM_SIZE</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ICM_PROFILE_NAME</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ICM_PROFILE_NAME</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ICM_PROFILE_NAME</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅注意： c</p></td>
<td><p>WIA_IPA_ICM_PROFILE_NAME</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_FILENAME_EXTENSION</p>
<p>只读访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_FILENAME_EXTENSION</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_FILENAME_EXTENSION</p>
<p>只读访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_FILENAME_EXTENSION</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_SUPPRESS_PROPERTY_PAGE</p>
<p>只读访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_SUPPRESS_PROPERTY_PAGE</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_SUPPRESS_PROPERTY_PAGE</p>
<p>只读访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_SUPPRESS_PROPERTY_PAGE</p>
<p>只读访问</p></td>
<td><p>放</p></td>
</tr>
<tr class="even">
<td><p>一般： WIA_CATEGORY_ROOT</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
<td><p>WIA_IPA_ITEM_CATEGORY</p>
<p>只读访问，请参阅备注： f</p></td>
<td><p>Root</p></td>
</tr>
<tr class="odd">
<td><p>一般： WIA_CATEGORY_FLATBED</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ITEM_CATEGORY</p>
<p>只读访问，请参阅备注： f</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="even">
<td><p>一般： WIA_CATEGORY_FEEDER</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_ITEM_CATEGORY</p>
<p>只读访问，请参阅备注： f</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES</p>
<p>只读访问，请参阅注意： l</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
<td><p>WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES</p>
<p>只读访问，请参阅注意： l</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_BUFFER_SIZE</p>
<p>只读访问，请参阅注意： l</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_BUFFER_SIZE</p>
<p>只读访问，请参阅注意： l</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_BUFFER_SIZE</p>
<p>只读访问，请参阅注意： l</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_BUFFER_SIZE</p>
<p>只读访问，请参阅注意： l</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_MIN_BUFFER_SIZE</p>
<p>只读访问，请参阅注意： l</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_MIN_BUFFER_SIZE</p>
<p>只读访问，请参阅注意： l</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_MIN_BUFFER_SIZE</p>
<p>只读访问，请参阅注意： l</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_MIN_BUFFER_SIZE</p>
<p>只读访问，请参阅注意： l</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_PIXELS_PER_LINE</p>
<p>只读访问，请参阅注意： m</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_PIXELS_PER_LINE</p>
<p>只读访问，请参阅注意： m</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_PIXELS_PER_LINE</p>
<p>只读访问，请参阅注意： m</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_PIXELS_PER_LINE</p>
<p>只读访问，请参阅注意： m</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_NUMBER_OF_LINES</p>
<p>只读访问，请参阅注意： m</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_NUMBER_OF_LINES</p>
<p>只读访问，请参阅注意： m</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_NUMBER_OF_LINES</p>
<p>只读访问，请参阅注意： m</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_NUMBER_OF_LINES</p>
<p>只读访问，请参阅注意： m</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_BYTES_PER_LINE</p>
<p>只读访问，请参阅注意： m</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_BYTES_PER_LINE</p>
<p>只读访问，请参阅注意： m</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_BYTES_PER_LINE</p>
<p>只读访问，请参阅注意： m</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_BYTES_PER_LINE</p>
<p>只读访问，请参阅注意： m</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_PLANAR</p>
<p>只读访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_PLANAR</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_PLANAR</p>
<p>只读访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPA_PLANAR</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_MAX_SCAN_TIME</p>
<p>只读访问</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
<td><p>WIA_DPS_MAX_SCAN_TIME</p>
<p>只读访问</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="note-a-"></a>注意 a：  
在 Windows XP 根项或子项 (WIA DPS 文档处理中， (ADF) 或进纸器上下文的进纸器项 \_ \_ \_ \_ 设置为 "馈送器) "。

<a href="" id="note-b-"></a>备注 b：  
Windows XP 根或子项目上的平板物品或平板上下文 (WIA \_ DPS \_ 文档 \_ 处理 \_ 选择设置为平板) 。

<a href="" id="note-c-"></a>备注 c：  
根项，没有为 Windows XP 指定的上下文。

<a href="" id="note-d-"></a>备注 d：  
由 WIA 服务管理。

<a href="" id="note-e-"></a>备注 e：  
自定义应用程序的应用程序项树 (-AIT) 。

<a href="" id="note-f-"></a>备注 f：  
即使在驱动程序的应用程序项树上不支持 (D-AIT) ，也添加到-AIT。 设置为 **WiaImgFmt \_ BMP**。

<a href="" id="note-g-"></a>备注 g：  
对于 Windows Vista 到 Windows XP 的翻译，添加要与 [TYMED \_ 回调](understanding-tymed.md)一起使用的 **WiaImgFmt \_ MEMORYBMP** 。

<a href="" id="note-h-"></a>备注 h：  
对于 Windows Vista 到 Windows XP 的翻译，请添加 TYMED \_ 回调和 **WiaImgFmt \_ MEMORYBMP**。 对于 Windows XP 到 Windows Vista 的翻译，只翻译 [TYMED \_ 文件](understanding-tymed.md) 和 TYMED \_ 多页 \_ 文件。

<a href="" id="note-i-"></a>请注意：  
对于 Windows XP 到 Windows Vista 的翻译，只翻译：

TYMED \_ 文件

TYMED \_ 多页 \_ 文件

注意 j：对于 Windows XP 到 Windows Vista 的翻译，只翻译：

重复

馈电

降

检测 \_ 源

检测 \_ 平面

检测 \_ 扫描

注意 k：即使在 D-AIT 上不支持，也可以添加到-AIT。 设置为 TYMED \_ 文件。

注意 l：即使在 D-AIT 上不支持，也可以添加到-AIT。

备注 m：对于所有启用了传输的设备，Windows Vista 都是可选的。 如果实现了这些属性，则旧应用程序可获取每行的像素数、每个扫描行所需的字节数，以及图像中的扫描行总数。 这些值不准确，因为图像处理筛选器可能会修改这些属性所表示的实际值。

如果 Windows Vista 驱动程序未提供这些属性，则 WIA 服务中的兼容性层将添加这些属性。 当 WIA 服务添加这些属性时，将使用属性： WIA \_ IPA \_ DEPTH、wia \_ IPS \_ XEXTENT 和 wia \_ ips \_ YEXTENT 来更新这些属性。

**注意**   如果可能，应用程序应始终分析图像标头数据，以获取有关映像的准确信息。 它们不应依赖于此属性，因为它不准确。

 

 

 




