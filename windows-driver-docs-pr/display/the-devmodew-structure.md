---
title: DEVMODEW 结构
description: DEVMODEW 结构
ms.assetid: 26212e3b-a591-4ed6-b441-b130d8d4d948
keywords:
- GDI WDK Windows 2000 显示，DEVMODEW 结构
- 图形驱动程序 WDK Windows 2000 显示，DEVMODEW 结构
- DEVMODEW 结构 WDK Windows 2000 显示
- Unicode WDK 图形
- 绘制 WDK GDI，DEVMODEW 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5faef4206ec7b7dab9117af7ed9cc2501caf4acd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542574"
---
# <a name="the-devmodew-structure"></a>DEVMODEW 结构


## <span id="ddk_the_devmodew_structure_gg"></span><span id="DDK_THE_DEVMODEW_STRUCTURE_GG"></span>


[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)结构是 Microsoft Windows SDK 文档中所述的 DEVMODE 结构的 Unicode 版本。 （DEVMODEW 上的 W 后缀表示"宽型"或 Unicode 字符。）虽然应用程序可以使用任一结构，使用 DEVMODEW 结构而不是 DEVMODE 结构需要驱动程序。

### <a name="span-idpublicandprivatemembersspanspan-idpublicandprivatemembersspanpublic-and-private-members"></a><span id="public_and_private_members"></span><span id="PUBLIC_AND_PRIVATE_MEMBERS"></span>公共和私有成员

立即遵循 DEVMODEW 结构的定义 （通常称为其公共 DEVMODEW 成员） 的成员，可以有一套驱动程序定义的成员 （其私有 DEVMODEW 成员）。 下图显示了公共部分 （实际 DEVMODEW 结构本身） 和专用部分。

![说明 devmodew 结构的公用和专用部分的关系图](images/devmode.png)

通常情况下，私有成员仅使用打印机驱动程序。 驱动程序提供的大小，以字节为单位，在此专用区域**dmDriverExtra**成员。 驱动程序定义的私有成员均为独占使用的驱动程序。

有关打印机驱动程序，DEVMODEW 结构用于指定打印文档的用户选项。 它还用于指定这些选项的打印机，如打印、 纸张大小的副本数和其他属性的默认值。 显示设备的 DEVMODEW 结构指定显示属性，如每个像素、 像素尺寸和显示频率比特数。

### <a name="span-idinitializingadevmodewstructurespanspan-idinitializingadevmodewstructurespaninitializing-a-devmodew-structure"></a><span id="initializing_a_devmodew_structure"></span><span id="INITIALIZING_A_DEVMODEW_STRUCTURE"></span>初始化 DEVMODEW 结构

根据它是用于显示驱动程序或打印机驱动程序，DEVMODEW 结构初始化两个不同的方式。

-   显示驱动程序 DEVMODEW 初始化

    显示驱动程序[ **DrvGetModes** ](https://msdn.microsoft.com/library/windows/hardware/ff556233)入口点初始化为零的 DEVMODEW 结构的所有成员。 *DrvGetModes*然后复制显示驱动程序 DLL 的名称为**dmDeviceName**成员，将填充**dmSpecVersion**并**dmDriverVersion**成员DEVMODEW 结构和副本的版本使用相应的成员来显示属性信息。

-   打印机驱动程序 DEVMODEW 初始化

    应用程序时进行调用**DocumentProperties** （打印机接口 DLL 函数的 Microsoft Windows SDK 文档中所述） 或[ **DrvDocumentPropertySheets**](https://msdn.microsoft.com/library/windows/hardware/ff548548) （基于 NT 的操作系统图形 DDI），使用默认值创建 DEVMODEW 结构。 然后，应用程序可以自由地修改任何公共 DEVMODEW 成员。 后任何更改，应用程序应请对它调用之前，以合并使用这些驱动程序的内部 DEVMODEW 结构已更改的成员的同一函数的第二个调用。 第二次调用是必要的因为某些更改可能无法正常运行;打印机驱动程序必须调用以更正 DEVMODEW 结构。 当文档要打印时，应用程序传递的合并的 DEVMODEW 结构**CreateDC** （Microsoft Windows SDK 文档中介绍），这将传递到[ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211) DDI。 此时，驱动程序的呈现 DLL 验证 DEVMODEW 结构，并会在修复，如有必要，然后才可执行打印作业。

### <a name="span-idusingadevmodewstructurespanspan-idusingadevmodewstructurespanusing-a-devmodew-structure"></a><span id="using_a_devmodew_structure"></span><span id="USING_A_DEVMODEW_STRUCTURE"></span>使用 DEVMODEW 结构

多个 Api 和图形 DDIs 为作为打印，并查询设备功能、 显示用户界面和其他此类目的 DEVMODEW 结构中使用的信息。 例如， [ **DrvConvertDevMode** ](https://msdn.microsoft.com/library/windows/hardware/ff548532)是转换到另一个操作系统版本从 DEVMODEW 结构 DDI 的打印后台处理程序图形。 这可能是必要的打印机驱动程序从不同的操作系统版本运行的另一台计算机获取 DEVMODEW 结构。

### <a name="span-idmodifyingadevmodewstructurespanspan-idmodifyingadevmodewstructurespanmodifying-a-devmodew-structure"></a><span id="modifying_a_devmodew_structure"></span><span id="MODIFYING_A_DEVMODEW_STRUCTURE"></span>修改 DEVMODEW 结构

应用程序和驱动程序可以随意提出 DEVMODEW 结构并直接修改其公共部分。 唯一的驱动程序，但是，有权修改专用 DEVMODEW 结构成员。

若要修改专用 DEVMODEW 结构成员，驱动程序必须首先确定专用数据的起始位置的偏移量。 提供指向此结构的开头的指针并**dmSize**成员，其中包含结构的公共部分的大小，可以找到的专用部分的开头。 下面的示例演示如何初始化到的专用部分开头的指针。 在此示例中， *pdm*指向 DEVMODEW 结构的开头。

```cpp
PVOID pvDriverData = (PVOID)  (((BYTE *) pdm) + (pdm -> dmSize));
```

### <a name="span-idprinterdriverdisplaydriverdevmodewdifferencesspanspan-idprinterdriverdisplaydriverdevmodewdifferencesspanprinter-driverdisplay-driver-devmodew-differences"></a><span id="printer_driver_display_driver_devmodew_differences"></span><span id="PRINTER_DRIVER_DISPLAY_DRIVER_DEVMODEW_DIFFERENCES"></span>打印机驱动程序/显示驱动程序 DEVMODEW 差异

DEVMODEW 结构成员划分为三个类别：

-   仅由打印机驱动程序的成员

-   成员仅供显示驱动程序

-   打印机和显示器驱动程序使用的成员

下表列出了几个使用公共 DEVMODEW 成员*仅*的打印机驱动程序：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DEVMODEW 成员仅由打印机驱动程序</th>
<th align="left">用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dmScale</strong></p></td>
<td align="left"><p>指定图像将进行缩放用于打印的百分比。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmCopies</strong></p></td>
<td align="left"><p>指定要打印的份数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dmColor</strong></p></td>
<td align="left"><p>指定是否彩色还是单色应打印彩色打印机。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmOrientation</strong></p></td>
<td align="left"><p>指定的纸张方向纵向或横向。</p></td>
</tr>
</tbody>
</table>

 

下一个表列出了几个使用公共 DEVMODEW 成员*仅*通过显示驱动程序：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DEVMODEW 成员仅由显示器驱动程序</th>
<th align="left">用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dmBitsPerPel</strong></p></td>
<td align="left"><p>指定的颜色分辨率，以每像素位数，显示设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmPelsWidth</strong></p></td>
<td align="left"><p>指定宽度，以像素为单位设备可视界面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dmPelsHeight</strong></p></td>
<td align="left"><p>指定高度，以像素为单位设备可视界面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmDisplayFlags</strong></p></td>
<td align="left"><p>指定的显示模式的颜色与单色，隔行扫描与非隔行扫描。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dmDisplayFrequency</strong></p></td>
<td align="left"><p>指定显示以赫兹，&#39;s 刷新频率。</p></td>
</tr>
</tbody>
</table>

 

第三个表列出了几个公共 DEVMODEW 成员由这两个打印机并显示驱动程序：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DEVMODEW 成员使用的打印机和显示器驱动程序</th>
<th align="left">用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dmDeviceName</strong></p></td>
<td align="left"><p>对于显示的指定显示驱动程序&#39;s DLL。</p>
<div>
 
</div>
对于打印机，指定&quot;友好名称&quot;的打印机。</td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmFields</strong></p></td>
<td align="left"><p>指定标识的 DEVMODEW 其后的成员正在使用的位标志。 例如，DM_BITSPERPEL 标志时设置<strong>dmBitsPerPel</strong>成员包含有效的数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dmSize</strong></p></td>
<td align="left"><p>指定的大小，以字节为单位的 DEVMODEW 结构的公共部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmDriverExtra</strong></p></td>
<td align="left"><p>指定以下公共结构成员的专用驱动程序数据的字节数。 显示驱动程序，这通常是零。</p></td>
</tr>
</tbody>
</table>

 

 

 





