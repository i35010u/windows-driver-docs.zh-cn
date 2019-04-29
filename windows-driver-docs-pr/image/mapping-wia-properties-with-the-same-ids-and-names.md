---
title: 映射具有相同 ID 和名称的 WIA 属性
description: 映射具有相同 ID 和名称的 WIA 属性
ms.assetid: 40a1094d-50fa-42b6-9976-ec6b05fdc384
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a9c3b2adbc9531b84e1920b2d4c80bb1140f0a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380364"
---
# <a name="mapping-wia-properties-with-the-same-ids-and-names"></a>映射具有相同 ID 和名称的 WIA 属性


没有具有相同的属性 Id 和属性名称与 Windows Vista 的 Windows XP 属性。 下面是这些 Windows XP 根属性以及它们在 Windows Vista 中将转换为的平板和送纸器 (ADF) 属性表。

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
<p><strong>项 / 上下文</strong></p></td>
<td><p><strong>Windows Vista 属性</strong></p></td>
<td><p><strong>Windows Vista 项目</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_NAME</p>
<p>只读访问权限，请参阅注意： d</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
<td><p>WIA_IPA_ITEM_NAME</p>
<p>只读访问权限，请参阅注意： d</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ITEM_NAME</p>
<p>或泛型："平板"</p>
<p>只读访问权限，请参阅说明： d 和 e</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ITEM_NAME</p>
<p>只读访问权限，请参阅说明： d 和 e</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_NAME</p>
<p>或泛型："送纸器"</p>
<p>只读访问权限，请参阅说明： d 和 e</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_ITEM_NAME</p>
<p>只读访问权限，请参阅说明： d 和 e</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>只读访问权限，请参阅注意： d</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>只读访问权限，请参阅注意： d</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>或泛型:"\Root\FLATBED"</p>
<p>只读访问权限，请参阅说明： d 和 e</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>或泛型:"\Root\FEEDER"</p>
<p>只读访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>只读访问权限，请参阅说明： d 和 e</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_TIME</p>
<p>只读访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ITEM_TIME</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ITEM_TIME</p>
<p>只读访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_ITEM_TIME</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>只读访问权限，请参阅说明： d 和 e</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>只读访问权限，请参阅说明： d 和 e</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>只读访问权限，请参阅说明： d 和 e</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>只读访问权限，请参阅说明： d 和 e</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>只读访问权限，请参阅说明： d 和 e</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>只读访问权限，请参阅说明： d 和 e</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>只读访问权限</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>只读访问权限</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>只读访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>只读访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_DATATYPE</p>
<p>请参阅备注： b</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_DATATYPE</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_DATATYPE</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_DATATYPE</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_DEPTH</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_DEPTH</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_DEPTH</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_DEPTH</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_PREFERRED_FORMAT</p>
<p>只读访问权限，请参阅注意： f</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_PREFERRED_FORMAT</p>
<p>只读访问权限，请参阅注意： f</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_PREFERRED_FORMAT</p>
<p>只读访问权限，请参阅注意： f</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_PREFERRED_FORMAT</p>
<p>只读访问权限，请参阅注意： f</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_FORMAT</p>
<p>读/写访问，请参阅说明： h 和我</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_FORMAT</p>
<p>读/写访问，请参阅说明： h 和我</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_FORMAT</p>
<p>读/写访问，请参阅说明： h 和我</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_FORMAT</p>
<p>读/写访问，请参阅说明： h 和我</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_COMPRESSION</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_COMPRESSION</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_COMPRESSION</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_COMPRESSION</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_TYMED</p>
<p>读/写访问，请参阅说明： h、 i 和 k</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_TYMED</p>
<p>读/写访问，请参阅说明： h、 i 和 k</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_TYMED</p>
<p>读/写访问，请参阅说明： h 和我</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_TYMED</p>
<p>读/写访问，请参阅说明： h 和我</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_CHANNELS_PER_PIXEL</p>
<p>只读访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_CHANNELS_PER_PIXEL</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_CHANNELS_PER_PIXEL</p>
<p>只读访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_CHANNELS_PER_PIXEL</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_BITS_PER_CHANNEL</p>
<p>只读访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_BITS_PER_CHANNEL</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_BITS_PER_CHANNEL</p>
<p>只读访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_BITS_PER_CHANNEL</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_SIZE</p>
<p>只读访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ITEM_SIZE</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ITEM_SIZE</p>
<p>只读访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_ITEM_SIZE</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ICM_PROFILE_NAME</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ICM_PROFILE_NAME</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ICM_PROFILE_NAME</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅备注： c</p></td>
<td><p>WIA_IPA_ICM_PROFILE_NAME</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_FILENAME_EXTENSION</p>
<p>只读访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_FILENAME_EXTENSION</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_FILENAME_EXTENSION</p>
<p>只读访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_FILENAME_EXTENSION</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_SUPPRESS_PROPERTY_PAGE</p>
<p>只读访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_SUPPRESS_PROPERTY_PAGE</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_SUPPRESS_PROPERTY_PAGE</p>
<p>只读访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_SUPPRESS_PROPERTY_PAGE</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p></td>
</tr>
<tr class="even">
<td><p>泛型：WIA_CATEGORY_ROOT</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
<td><p>WIA_IPA_ITEM_CATEGORY</p>
<p>只读访问权限，请参阅注意： f</p></td>
<td><p>根</p></td>
</tr>
<tr class="odd">
<td><p>泛型：WIA_CATEGORY_FLATBED</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_ITEM_CATEGORY</p>
<p>只读访问权限，请参阅注意： f</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="even">
<td><p>泛型：WIA_CATEGORY_FEEDER</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_ITEM_CATEGORY</p>
<p>只读访问权限，请参阅注意： f</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES</p>
<p>只读访问权限，请参阅注意： l</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
<td><p>WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES</p>
<p>只读访问权限，请参阅注意： l</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_BUFFER_SIZE</p>
<p>只读访问权限，请参阅注意： l</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_BUFFER_SIZE</p>
<p>只读访问权限，请参阅注意： l</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_BUFFER_SIZE</p>
<p>只读访问权限，请参阅注意： l</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_BUFFER_SIZE</p>
<p>只读访问权限，请参阅注意： l</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_MIN_BUFFER_SIZE</p>
<p>只读访问权限，请参阅注意： l</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_MIN_BUFFER_SIZE</p>
<p>只读访问权限，请参阅注意： l</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_MIN_BUFFER_SIZE</p>
<p>只读访问权限，请参阅注意： l</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_MIN_BUFFER_SIZE</p>
<p>只读访问权限，请参阅注意： l</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_PIXELS_PER_LINE</p>
<p>只读访问权限，请参阅注意： m</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_PIXELS_PER_LINE</p>
<p>只读访问权限，请参阅注意： m</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_PIXELS_PER_LINE</p>
<p>只读访问权限，请参阅注意： m</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_PIXELS_PER_LINE</p>
<p>只读访问权限，请参阅注意： m</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_NUMBER_OF_LINES</p>
<p>只读访问权限，请参阅注意： m</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_NUMBER_OF_LINES</p>
<p>只读访问权限，请参阅注意： m</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_NUMBER_OF_LINES</p>
<p>只读访问权限，请参阅注意： m</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_NUMBER_OF_LINES</p>
<p>只读访问权限，请参阅注意： m</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_BYTES_PER_LINE</p>
<p>只读访问权限，请参阅注意： m</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_BYTES_PER_LINE</p>
<p>只读访问权限，请参阅注意： m</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_BYTES_PER_LINE</p>
<p>只读访问权限，请参阅注意： m</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_BYTES_PER_LINE</p>
<p>只读访问权限，请参阅注意： m</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_PLANAR</p>
<p>只读访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPA_PLANAR</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_PLANAR</p>
<p>只读访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPA_PLANAR</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_MAX_SCAN_TIME</p>
<p>只读访问权限</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
<td><p>WIA_DPS_MAX_SCAN_TIME</p>
<p>只读访问权限</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="note-a-"></a>请注意答：  
送纸器项 (ADF) 或 Windows XP 根或子项目上的送纸器上下文 (WIA\_DPS\_文档\_处理\_选择设置为送纸器)。

<a href="" id="note-b-"></a>请注意 b:  
平板项或 Windows XP 根或子项目上的平板上下文 (WIA\_DPS\_文档\_处理\_选择设置为平板)。

<a href="" id="note-c-"></a>请注意 c:  
根项中，指定适用于 Windows XP 没有上下文。

<a href="" id="note-d-"></a>请注意 d:  
服务管理的 WIA。

<a href="" id="note-e-"></a>请注意 e:  
为应用程序的应用程序项树 (一个 AIT) 自定义。

<a href="" id="note-f-"></a>请注意 f:  
将添加到一个 AIT 即使驱动程序的应用程序项树 (D AIT) 上不受支持。 设置为**WiaImgFmt\_BMP**。

<a href="" id="note-g-"></a>请注意 g:  
对于 Windows XP 转换到 Windows Vista 中，添加**WiaImgFmt\_MEMORYBMP**要用于[TYMED\_回调](understanding-tymed.md)。

<a href="" id="note-h-"></a>请注意 h:  
对于 Windows XP 转换到 Windows Vista 中，添加 TYMED\_回调并**WiaImgFmt\_MEMORYBMP**。 对于 Windows XP 到 Windows Vista，仅翻译[TYMED\_文件](understanding-tymed.md)和 TYMED\_多页\_转换文件。

<a href="" id="note-i-"></a>请注意实现：  
为 Windows XP 到 Windows Vista 的翻译，翻译仅：

TYMED\_文件

TYMED\_多页\_文件

请注意 j:为 Windows XP 到 Windows Vista 的翻译，翻译仅：

DUP

源

平面

检测\_源

检测\_平面

检测\_扫描

请注意 k:将添加到一个 AIT 即使 D AIT 上不受支持。 设置为 TYMED\_文件。

请注意 l:将添加到一个 AIT 即使 D AIT 上不受支持。

请注意 m:适用于 Windows Vista 的所有传输启用设备的可选。 如果实现了这些属性，旧版应用程序可以获得的每行，每个扫描行和在图像中扫描的总行数所需的字节数的像素数的估计值。 这些值不准确，因为图像处理筛选器可能会更改这些属性表示的实际值。

如果由 Windows Vista 驱动程序不提供这些属性，WIA 服务中的兼容性层将添加这些属性。 这些属性添加由 WIA 服务时，他们将使用属性进行更新：WIA\_IPA\_深度、 WIA\_IPS\_大 XEXTENT 和 WIA\_IP\_YEXTENT。

**请注意**  在可能的情况下，应用程序应始终分析映像标头数据，以获取有关映像的准确信息。 它们不应依赖于此属性，因为它不准确。

 

 

 




