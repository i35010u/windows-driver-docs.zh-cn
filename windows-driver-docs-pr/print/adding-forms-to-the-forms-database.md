---
title: 将表单添加到表单数据库
description: 将表单添加到表单数据库
ms.assetid: ac306f05-6150-4e47-9272-e81e658a1ea6
keywords:
- 附加的窗体 WDK Unidrv
- 将窗体添加到 Unidrv 打印机驱动程序
- Unidrv，窗体添加到数据库
- GPD 文件 WDK Unidrv 窗体添加到数据库
- 打印机纸张规格 WDK
- 窗体 WDK 打印机
- 特殊的窗体 WDK 打印机
- 特殊纸张大小 WDK 打印机
- 纸张大小 WDK 窗体
- 自定义窗体 WDK 打印机
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ecb360b6f22e8154afd27a43fecbf21d0bfd35e
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349298"
---
# <a name="adding-forms-to-the-forms-database"></a>将表单添加到表单数据库


如果您的打印机支持附加的窗体，可以直接将它们添加到 Unidrv 打印机驱动程序，通过描述打印机驱动程序的 GPD 文件中。 如果你使用的资源 ID \*rcNameId 字段和资源 DLL 在窗体的显示名称字符串，您的驱动程序将自动使用新本地化的增强功能提供的功能的 Windows Vista Unidrv 打印机驱动程序。 Unidrv 打印机驱动程序插件还会自动受益于这些更改到后台处理程序并不需要任何其他修改。 有关这些增强功能的详细信息，请参阅[更改为 Windows Vista 中的打印机纸张规格](changes-to-printer-forms-in-windows-vista.md)。

如果您不将用于 GPD 文件中的可本地化字符串的资源 DLL，应删除可本地化的字符串、 将其存储在资源 DLL，和字符串替换为 GPD 文件中的相应资源 ID。

下面的代码示例摘自的显示名称中使用的资源 ID 的 GPD 文件。

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

Windows vista 中，在窗体提供 Unidrv 打印机驱动程序内\_信息\_2 结构是否填充的从文件中读取 GPD，如下表所示的数据。 如果您的打印机的 GPD 文件已包含在此结构中填充所需的信息，请不需要进行任何更改即可使用 Windows Vista Unidrv 打印机驱动程序提供的新功能。

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
<th>使用 GPD 值</th>
<th>字段说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Flags</p></td>
<td><p>FORM_PRINTER</p>
<p>此值是由 Unidrv 打印机驱动程序分配，因为它添加窗体。 为此字段不使用 GPD 文件中的值。</p></td>
<td><p>结构的属性。</p></td>
</tr>
<tr class="even">
<td><p>pName</p></td>
<td><p>获取从资源 DLL 或从窗体的本地化的名称 * rcName GPD 文件中的字段。</p></td>
<td><p>指向一个以 null 结尾的字符串，指定格式的名称的指针。 此字符串用于标识窗体数据库中的窗体，必须是唯一的。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>大小信息从读取 * PageDimensions GPD 文件中的选项。</p></td>
<td><p>宽度和高度，以毫米为单位，窗体的千分之几秒。</p></td>
</tr>
<tr class="even">
<td><p>ImageableArea</p></td>
<td><p>大小信息从读取 * PrintableArea GPD 文件中的选项。</p></td>
<td><p>宽度和高度，以毫米为单位的打印机可以打印的页面区域的千分之几秒。</p></td>
</tr>
<tr class="odd">
<td><p>pKeyword</p></td>
<td><p>值 * 选项 GPD 文件中的条目。</p></td>
<td><p>一个指向该窗体的非可本地化的字符串标识符。 传递到 AddForm 或 SetForm 时，此指针，调用方可以识别的窗体中的所有区域设置。</p></td>
</tr>
<tr class="even">
<td><p>StringType</p></td>
<td><p>STRING_MUIDLL</p>
<p>如果使用 GPD * rcNameId 选项和窗体名称为可从资源 DLL，STRING_MUIDLL 赋值。 如果 * rcName 选项改为使用 GPD 文件中，此字段的值为 STRING_NONE。 为此字段不使用 GPD 文件中的值。</p></td>
<td><p>指定如何在运行时获取窗体的本地化的显示名称。</p></td>
</tr>
<tr class="odd">
<td><p>pMuiDll</p></td>
<td><p>值 * 文件中 GPD 项 ResourceDLL 项，如果 * 使用 rcNameId 选项。 如果 * rcName 选项改为使用 GPD 文件中，此字段的值是<strong>NULL</strong>。</p></td>
<td><p>MUI 本地化资源 DLL，其中包含本地化的显示名称时<strong>StringType</strong>包含 STRING_MUIDLL。</p></td>
</tr>
<tr class="even">
<td><p>dwResourceId</p></td>
<td><p>值 * rcNameID GPD 文件中的条目。 如果 * rcName 选项改为使用 GPD 文件中，此字段的值为 0。</p></td>
<td><p>资源 ID <strong>pMuiDll</strong>的窗体的显示名称时<strong>StringType</strong>包含 STRING_MUIDLL。</p></td>
</tr>
<tr class="odd">
<td><p>pDisplayName</p></td>
<td><p><strong>NULL</strong></p>
<p>不使用此字段。</p></td>
<td><p>在语言中的窗体的显示名称的<strong>wLangId</strong>指定何时<strong>StringType</strong>包含 STRING_LANGPAIR。</p></td>
</tr>
<tr class="even">
<td><p>wLangId</p></td>
<td><p>0</p>
<p>不使用此字段。</p></td>
<td><p>语言<strong>pDisplayName</strong>时<strong>StringType</strong>包含 STRING_LANGPAIR。</p></td>
</tr>
</tbody>
</table>

 

 

 




