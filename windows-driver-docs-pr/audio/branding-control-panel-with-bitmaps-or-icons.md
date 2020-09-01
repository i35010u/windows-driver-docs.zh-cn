---
title: 使用位图或图标打造控件面板的品牌
description: 使用位图或图标打造控件面板的品牌
ms.assetid: 1520cf9e-6813-41aa-aa88-39a1a6c27f74
keywords:
- 音频适配器 WDK，控制面板品牌
- 适配器驱动程序 WDK 音频、控制面板品牌
- 端口类音频适配器 WDK，控制面板品牌
- 控制面板品牌 WDK 音频
- 品牌设备控制 WDK 音频
- 第三方署名 WDK 音频
- 供应商品牌 WDK 音频
- 徽标品牌 WDK 音频
- 图标 WDK 音频
- 位图品牌音响音频
- 图像品牌 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6641b1b7f2e639f583dc15955430632a2a0ca792
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208223"
---
# <a name="branding-control-panel-with-bitmaps-or-icons"></a>使用位图或图标打造控件面板的品牌


## <span id="control_panel_branding_by_vendors"></span><span id="CONTROL_PANEL_BRANDING_BY_VENDORS"></span>


在 Windows XP 和更高版本的 Windows 中，控制面板中的声音应用程序支持音频设备控件的第三方品牌标记。 独立硬件供应商 (Ihv) 可以在其音频设备的控件旁边显示以下各项：

-   公司徽标

-   专用设备名称

安装设备驱动程序的 INF 文件还会将控制面板自定义数据加载到注册表中。 公司徽标的位图图像包含在已安装的驱动程序文件中。

在 Windows XP 中，用户可以在以下程序位置看到品牌信息：

-   "控制面板" 中 "**声音和音频设备**" 应用程序的 "**卷**" 页 ( # A0) 

-   SndVol32 程序 ( # A0) 

在 Windows Vista 中，用户可以在 "控制面板" 中的*声音*应用程序的 "**播放**和**记录**" 页中查看品牌信息 ( # A0) 。

品牌信息存储在音频设备根密钥下的 **署名** 子项下的注册表中，该根密钥位于 media 类键下。 **品牌**子项可包含下表中显示的一个或多个 REG \_ SZ 值。

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
<td align="left"><p>icon</p></td>
<td align="left"><p>包含 SndVol32 控件菜单所使用的图标的文件的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>位图</p></td>
<td align="left"><p>文件的名称，该文件包含在 "控制面板" 的 "<strong>声音和音频设备</strong>" 应用程序的 "<strong>卷</strong>" 页中显示的 32 x 32 位图。</p></td>
</tr>
</tbody>
</table>

 

这些值通过 "添加注册表"-部分中的指令添加到注册表中 (参阅 [**Inf AddReg 指令**](../install/inf-addreg-directive.md)) 安装设备驱动程序的 inf 文件。 控制面板对 **品牌** 子项中缺少的任何值使用默认值。

"位图" 徽标出现在 " **卷** " 页面顶部专用设备名称的左侧。 "图标" 徽标显示在 SndVol32 控件菜单的左上角。

前面提到的页面中显示的专有设备名称是设备的友好名称。 此友好名称由安装设备的 INF 文件的 "添加注册表" 部分中的指令指定。 此指令包含关键字 "FriendlyName"，如 [**INF AddReg 指令**](../install/inf-addreg-directive.md)中的示例中所示。 在 Windows XP 中，" **卷** " 页和 SndVol32 仅显示名称字符串的前31个字符。 超过最大长度的字符串会被截断。 在 Windows Vista 和更高版本的 Windows 中，当设备名称显示在 "控制面板" 中时，将删除此31个字符的限制。 使用早于 Windows Vista 的 Windows 版本（例如 [MCI \_ GetDevCaps](/windows/win32/multimedia/mci-getdevcaps)）所支持的 api 时，31字符限制仍适用于你向 API 提供的设备名称。

**重要提示**   在 Windows Vista 和更高版本的 Windows 中，不再支持使用第三方品牌的位图图像。 要品牌音频设备控制的第三方音频驱动程序开发人员必须使用图标。 这些图标支持的像素尺寸为32x32 或48x48。

 

### <a name="span-idexample_1spanspan-idexample_1spanspan-idexample_1spanexample-1"></a><span id="Example_1"></span><span id="example_1"></span><span id="EXAMPLE_1"></span>示例1

下面的示例显示了来自供应商 INF 文件的 "添加注册表" 部分的几个指令：

```inf
  [XYZ-Audio-Device.AddReg]
  HKR,Branding,icon,,"foo.sys,102"
  HKR,Branding,bitmap,,"c:\mydir\myimage.bmp"
```

这些指令将控制面板品牌信息添加到注册表。 HKR 表示音频设备在注册表中的根密钥;指定 **品牌** 子项是相对于根密钥的路径名称指定的。 可以采用以下两种格式之一指定 **图标** 或 **位图** 键的字符串值： "file，resourceid" 或 "imagefile"。 前面的示例中的第一个指令使用 "文件，resourceid" 格式。 指令将一个字符串值分配给 **icon** 键，其中包含文件名、foo.sys 和资源 ID 102。 文件名和资源 ID 之间用逗号分隔，不能包含空格)  (。 文件 foo.sys 包含图标资源。 前面的示例中的第二个指令将 "imagefile" 格式的字符串分配给 **位图** 键;字符串包含包含位图的 .bmp 文件的完整路径名。

可以将 **图标** 值的示例指令更改为使用 "imagefile" 格式，但在这种情况下，字符串值应包含带有 .ico 文件扩展名的文件的路径名称。

对于 "文件，resourceid" 格式，控制面板软件会搜索相同的搜索路径列表，如 Microsoft Windows SDK 文档) ** (所述** 。 如果此路径列表中不包含该文件，则该软件还会搜索驱动程序目录 (参阅 [**INF DestinationDirs 部分**](../install/inf-destinationdirs-section.md)) 。 这种格式使得映像无需在 INF 文件中指定绝对路径名称，即可轻松地将其存储在驱动程序文件中。

### <a name="span-idexample_2spanspan-idexample_2span-example-2"></a><span id="example_2"></span><span id="EXAMPLE_2"></span> 示例 2

以下示例适用于 windows Vista 和更高版本的 Windows。 此示例显示供应商 INF 文件的 "外接程序" 部分中的指令。 此示例使用 "imagefile" 格式：

```inf
[ABC-Audio-Device.AddReg]
  HKR,Branding,icon,,"c:\mydir\myicon.ico"
```

 

