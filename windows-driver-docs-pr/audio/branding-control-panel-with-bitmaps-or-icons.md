---
title: 使用位图或图标打造控件面板的品牌
description: 使用位图或图标打造控件面板的品牌
ms.assetid: 1520cf9e-6813-41aa-aa88-39a1a6c27f74
keywords:
- 音频适配器 WDK，控件面板品牌
- 适配器驱动程序 WDK 音频控件面板品牌
- 端口类音频适配器 WDK，控件面板品牌
- 控件面板品牌 WDK 音频
- 品牌设备控件 WDK 音频
- 第三方品牌 WDK 音频
- 供应商品牌 WDK 音频
- 徽标品牌 WDK 音频
- 图标 WDK 音频
- 位图品牌 WDK 音频
- 映像品牌 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1270c27fa33320da4e67627a07d9051f0de356e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333894"
---
# <a name="branding-control-panel-with-bitmaps-or-icons"></a>使用位图或图标打造控件面板的品牌


## <span id="control_panel_branding_by_vendors"></span><span id="CONTROL_PANEL_BRANDING_BY_VENDORS"></span>


在 Windows XP 和更高版本的 Windows，控制面板中的声音应用程序支持的音频设备控件的第三方品牌。 独立硬件供应商 (Ihv) 可以显示为其音频设备控件旁边的以下项：

-   公司徽标

-   专用设备名称

安装设备驱动程序的 INF 文件还将控件面板自定义数据加载到注册表。 公司徽标位图化图像包含在已安装的驱动程序文件本身中。

在 Windows XP 中，品牌信息是对以下程序位置的用户可见：

-   **卷**页**声音和音频设备**控制面板 (Mmsys.cpl) 中应用程序

-   SndVol32 程序 (Sndvol32.exe)

在 Windows Vista 中，品牌信息是对中的用户可见**播放**并**录制**页*声音*控制面板 (Mmsys.cpl) 中应用程序。

品牌信息存储在注册表中**品牌**子项下媒体类键的音频设备的根项下。 **品牌**子项可以包含一个或多个 REG\_SZ 下表中所示的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值名称</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>图标</p></td>
<td align="left"><p>包含由 SndVol32 控制菜单的图标的文件的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>bitmap</p></td>
<td align="left"><p>包含 32 × 32 位图中显示的文件的名称<strong>卷</strong>页<strong>声音和音频设备</strong>控制面板中的应用程序。</p></td>
</tr>
</tbody>
</table>

 

这些值由指令中添加注册表部分添加到注册表 (请参阅[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)) 的安装设备驱动程序的 INF 文件。 控制面板中缺少任何值使用默认值**品牌**子项。

"Bitmap"徽标显示在顶部的专有设备名称的左侧**卷**页。 "图标"徽标出现在 SndVol32 控制菜单的左上角。

前面提到的页中显示的专有设备名称是设备的友好名称。 由安装在设备的 INF 文件的添加注册表部分中的指令指定此友好名称。 此指令中包含的关键字"FriendlyName"中的示例中所示[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)。 在 Windows XP 中，**卷**页和 SndVol32 显示只有名称字符串的前 31 个字符。 较长的字符串将被截断。 在 Windows Vista 和更高版本的 Windows 中，在控制面板中显示设备名称时删除此 31 个字符限制。 当你使用 Api 中受支持的 Windows 版本早于 Windows Vista，例如[MCI\_GetDevCaps](https://go.microsoft.com/fwlink/p/?linkid=149692)，31 个字符的限制仍然适用于 api 提供的设备名称。

**重要**  在 Windows Vista 和更高版本的 Windows，利用位图图像，对于第三方品牌不再受支持。 第三方音频驱动程序开发人员想要设置其音频设备控件的外观必须使用的图标。 这些图标的受支持的像素尺寸为 32 x 32 或 48 x 48。

 

### <a name="span-idexample1spanspan-idexample1spanspan-idexample1spanexample-1"></a><span id="Example_1"></span><span id="example_1"></span><span id="EXAMPLE_1"></span>示例 1

下面的示例显示了几个指令从供应商的 INF 文件的添加注册表部分：

```inf
  [XYZ-Audio-Device.AddReg]
  HKR,Branding,icon,,"foo.sys,102"
  HKR,Branding,bitmap,,"c:\mydir\myimage.bmp"
```

这些指令将控件面板品牌信息添加到注册表。 HKR 表示音频设备的根注册表项的;**品牌**子项指定相对于根项的路径名称。 字符串值**图标**或**位图**密钥可以指定在两种格式之一:"文件，资源 id"或"imagefile"。 在前面的示例的第一个指令使用"文件，资源 id"格式。 该指令将分配给**图标**密钥包含文件名称、 foo.sys 和 102 的资源 ID 的字符串值。 （使用无空格） 以逗号分隔的文件名称和资源 ID。 文件 foo.sys 包含图标资源。 在前面的示例将"imagefile"格式字符串中的第二个指令**位图**密钥; 该字符串包含一个包含位图的.bmp 文件的完整路径名称。

示例指令**图标**值可以改为使用"imagefile"格式，但在这种情况下的字符串值应包含扩展名为.ico 文件的路径名称。

在"文件，资源 id"格式的情况下控件面板软件在列表中搜索相同的搜索路径设置为**LoadLibrary**函数 （Microsoft Windows SDK 文档中所述）。 如果此路径列表不包含该文件，该软件还会搜索的驱动程序目录 (请参阅[ **INF DestinationDirs 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547383))。 此格式，可以轻松地将存储在驱动程序文件本身而无需在 INF 文件中指定绝对路径名称中的映像。

### <a name="span-idexample2spanspan-idexample2span-example-2"></a><span id="example_2"></span><span id="EXAMPLE_2"></span> 示例 2

下面的示例适用于 Windows Vista 和更高版本的 Windows。 此示例演示从供应商的 INF 文件的添加注册表部分的指令。 此示例使用"imagefile"格式：

```inf
[ABC-Audio-Device.AddReg]
  HKR,Branding,icon,,"c:\mydir\myicon.ico"
```

 

 




