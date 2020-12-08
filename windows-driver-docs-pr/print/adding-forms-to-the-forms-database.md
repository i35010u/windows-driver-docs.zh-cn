---
title: 将表单添加到表单数据库
description: 将表单添加到表单数据库
keywords:
- 其他表单 WDK Unidrv
- 将窗体添加到 Unidrv 打印机驱动程序
- Unidrv，添加到数据库的窗体
- GPD 文件 WDK Unidrv，已添加到数据库的窗体
- 打印机窗体 WDK
- forms WDK 打印机
- 特殊形式 WDK 打印机
- 特殊纸张大小 WDK 打印机
- 纸张大小 WDK 窗体
- 自定义表单 WDK 打印机
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cf2a6e24207f8d5d2821f842b21ad4c908bbc41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794229"
---
# <a name="adding-forms-to-the-forms-database"></a>将表单添加到表单数据库


如果打印机支持其他纸张规格，可以通过在打印机驱动程序的 GPD 文件中对其进行描述，将它们添加到 Unidrv 打印机驱动程序。 如果使用具有 rcNameId 字段的资源 ID \* 和用于窗体显示名称字符串的资源 DLL，则驱动程序将自动使用 Windows Vista Unidrv 打印机驱动程序提供的新本地化增强功能。 Unidrv 打印机驱动程序插件还会自动受益于对后台处理程序所做的更改，无需任何其他修改。 有关这些增强功能的详细信息，请参阅 [Windows Vista 中的打印机窗体更改](changes-to-printer-forms-in-windows-vista.md)。

如果未对 GPD 文件中的可本地化字符串使用资源 DLL，则应删除可本地化的字符串，将它们存储在资源 DLL 中，并将字符串替换为 GPD 文件中的相应资源 ID。

下面的代码示例摘自 GPD 文件，该文件使用显示名称的资源 ID。

```GDL
*Feature: PaperSize
{
    *Option: Option2
    {
 *rcNameID: 259
        (form definition)
    }
    (other form definitions).
}
```

在随 Windows Vista 一起提供的 Unidrv 打印机驱动程序中，表单 \_ INFO \_ 2 结构由从 GPD 文件中读取的数据进行填充，如下表所示。 如果打印机的 GPD 文件中已包含填充此结构所需的信息，则无需更改任何内容即可使用 Windows Vista Unidrv 打印机驱动程序提供的新功能。

```cpp
typedef struct _FORM_INFO_2 { 
  DWORD    Flags; 
  LPTSTR   pName; 
  SIZEL    Size; 
  RECTL    ImageableArea;
  LPCSTR   pKeyword;
  DWORD    StringType;
  LPCTSTR  pMuiDll;
  DWORD    dwResourceId;
  LPCTSTR  pDisplayName;
  LANGID   wLangId; 
} FORM_INFO_2, *PFORM_INFO_2;
```

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>FORM_INFO_2 字段</th>
<th>使用的 GPD 值</th>
<th>字段说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Flags</p></td>
<td><p>FORM_PRINTER</p>
<p>此值由 Unidrv 打印机驱动程序分配，因为它将添加窗体。 GPD 文件中的值不用于此字段。</p></td>
<td><p>结构的属性。</p></td>
</tr>
<tr class="even">
<td><p>pName</p></td>
<td><p>从资源 DLL 或 GPD 文件中的 * rcName 字段获取的窗体的本地化名称。</p></td>
<td><p>指向以 null 结尾的字符串的指针，该字符串指定窗体的名称。 此字符串用于标识 forms 数据库中的表单，并且必须是唯一的。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>从 GPD 文件中的 * PageDimensions 选项读取的大小信息。</p></td>
<td><p>窗体的宽度和高度（以毫米为单位）。</p></td>
</tr>
<tr class="even">
<td><p>ImageableArea</p></td>
<td><p>从 GPD 文件中的 * PrintableArea 选项读取的大小信息。</p></td>
<td><p>打印机可以打印的页面区域的宽度和高度（以毫米为单位）。</p></td>
</tr>
<tr class="odd">
<td><p>pKeyword</p></td>
<td><p>GPD 文件中的 * 选项项的值。</p></td>
<td><p>指向窗体的不可本地化字符串标识符的指针。 传递给 AddForm 或 SetForm 时，此指针向调用方提供一种在所有区域设置中标识窗体的方法。</p></td>
</tr>
<tr class="even">
<td><p>StringType</p></td>
<td><p>STRING_MUIDLL</p>
<p>如果 GPD 使用 * rcNameId 选项，并且可以从资源 DLL 中获取窗体名称，则会分配 STRING_MUIDLL 值。 如果改为在 GPD 文件中使用 * rcName 选项，则 STRING_NONE 此字段的值。 GPD 文件中的值不用于此字段。</p></td>
<td><p>指定在运行时如何获取窗体的本地化显示名称。</p></td>
</tr>
<tr class="odd">
<td><p>pMuiDll</p></td>
<td><p>如果使用 * rcNameId 选项，则为 GPD 文件中的 * ResourceDLL 项的值。 如果改为在 GPD 文件中使用 * rcName 选项，则此字段的值为 <strong>NULL</strong>。</p></td>
<td><p>MUI 本地化资源 DLL，其中包含 <strong>StringType</strong> 包含 STRING_MUIDLL 时的本地化显示名称。</p></td>
</tr>
<tr class="even">
<td><p>dwResourceId</p></td>
<td><p>GPD 文件中的 * rcNameID 项的值。 如果改为在 GPD 文件中使用 * rcName 选项，则此字段的值为0。</p></td>
<td><p><strong>StringType</strong>包含 STRING_MUIDLL 时窗体的显示名称的资源 ID （ <strong>pMuiDll</strong>）。</p></td>
</tr>
<tr class="odd">
<td><p>pDisplayName</p></td>
<td><p><strong>NULL</strong></p>
<p>不使用此字段。</p></td>
<td><p>窗体的显示名称，采用 <strong>wLangId</strong> 指定的语言， <strong>StringType</strong> 包含 STRING_LANGPAIR。</p></td>
</tr>
<tr class="even">
<td><p>wLangId</p></td>
<td><p>0</p>
<p>不使用此字段。</p></td>
<td><p>当<strong>StringType</strong>包含 STRING_LANGPAIR 时的<strong>pDisplayName</strong>的语言。</p></td>
</tr>
</tbody>
</table>

 

 

 




