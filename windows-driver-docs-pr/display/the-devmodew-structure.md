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
ms.openlocfilehash: f2983e851fafef1a3aed4cee99ca63c1d8a20b10
ms.sourcegitcommit: abe7fe9f3fbee8d12641433eeab623a4148ffed3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92185197"
---
# <a name="the-devmodew-structure"></a>DEVMODEW 结构

[**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew)结构是 DEVMODE 结构的 Unicode 版本，如 Microsoft Windows SDK 文档中所述。  ("DEVMODEW" 上的 "W" 后缀表示 "宽" 或 Unicode 字符。 ) 虽然应用程序可以使用这两种结构，但驱动程序需要使用 DEVMODEW 结构，而不是 DEVMODE 结构。

## <a name="public-and-private-members"></a>公有和私有成员

紧跟 DEVMODEW 结构的定义成员后 (通常称为其公共 DEVMODEW 成员) ，可以有一组 (其专用 DEVMODEW 成员) 的驱动程序定义成员。 下图显示了 (实际 DEVMODEW 结构自身) 和私有部分的公共部分。

![说明 devmodew 结构的公共和私有部分的示意图](images/devmode.png)

通常，专用成员仅用于打印机驱动程序。 驱动程序提供 **dmDriverExtra** 成员中此专用区域的大小（以字节为单位）。 驱动程序定义的私有成员专用于驱动程序。

对于打印机驱动程序，DEVMODEW 结构用于指定打印文档的用户选择。 它还用于为打印机指定这些选项的默认值，例如要打印的份数、纸张大小和其他属性。 对于显示设备，DEVMODEW 结构指定显示属性，如每个像素的位数、像素维度和显示频率。

## <a name="initializing-a-devmodew-structure"></a>初始化 DEVMODEW 结构

根据显示驱动程序或打印机驱动程序的使用情况，将以两种不同的方式初始化 DEVMODEW 结构。

- 显示驱动程序 DEVMODEW 初始化

  显示驱动程序的 [**DrvGetModes**](/windows/win32/api/winddi/nf-winddi-drvgetmodes) 入口点将 DEVMODEW 结构的所有成员初始化为零。 然后， *DrvGetModes*将显示驱动程序 DLL 的名称复制到**dmDeviceName**成员，用 DEVMODEW 结构的版本填充**dmSpecVersion**和**dmDriverVersion**成员，并将显示属性信息复制到相应成员。

- 打印机驱动程序 DEVMODEW 初始化

  当应用程序调用 **DocumentProperties** (打印机接口 DLL 函数（在 Microsoft Windows SDK 文档) 或 [**DRVDOCUMENTPROPERTYSHEETS**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets) (基于 NT 的操作系统图形 DDI) 中介绍）时，将使用默认值创建 DEVMODEW 结构。 然后，应用程序可以自由修改任何公用 DEVMODEW 成员。 在进行任何更改后，应用程序随后应对它调用的同一函数进行第二次调用，以便将已更改的成员与驱动程序的内部 DEVMODEW 结构的成员合并。 第二次调用是必需的，因为某些更改可能无法正常工作;若要更正 DEVMODEW 结构，必须调用打印机驱动程序。 打印文档时，应用程序会将合并的 DEVMODEW 结构传递到 Microsoft Windows SDK 文档) 中所述的 **CreateDC** (，并将其传递到 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) DDI。 当时，驱动程序的呈现 DLL 会在执行打印作业之前验证 DEVMODEW 结构并进行修复（如有必要）。

## <a name="using-a-devmodew-structure"></a>使用 DEVMODEW 结构

许多 Api 和图形 DDIs 使用 DEVMODEW 结构中的信息来实现此目的，如打印、查询设备功能、显示用户界面等。 例如， [**DrvConvertDevMode**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvconvertdevmode) 是将 DEVMODEW 结构从一个操作系统版本转换到另一个版本的打印后台处理程序图形 DDI。 如果打印机驱动程序从另一台运行在不同操作系统版本上的计算机获取 DEVMODEW 结构，则可能需要执行此操作。

## <a name="modifying-a-devmodew-structure"></a>修改 DEVMODEW 结构

应用程序和驱动程序可自由请求 DEVMODEW 结构并直接修改其公共部件。 不过，只有驱动程序才允许修改私有 DEVMODEW 结构成员。

为了修改 private DEVMODEW 结构成员，驱动程序必须首先确定专用数据开始处的偏移量。 给定指向此结构的开头的指针，并在 **dmSize** 成员（它包含结构的公共部分的大小）中找到该私有部分的开头。 下面的示例演示如何初始化指向私有部分开头的指针。 在此示例中， *pdm* 指向 DEVMODEW 结构的开头。

```cpp
PVOID pvDriverData = (PVOID)  (((BYTE *) pdm) + (pdm -> dmSize));
```

## <a name="printer-driverdisplay-driver-devmodew-differences"></a>打印机驱动程序/显示器驱动程序 DEVMODEW 差异

DEVMODEW 结构成员分为三个类别：

- 仅供打印机驱动程序使用的成员

- 仅显示驱动程序使用的成员

- 打印机和显示器驱动程序使用的成员

下表列出了一些 *仅* 供打印机驱动程序使用的公共 DEVMODEW 成员：

| 仅供打印机驱动程序使用 | 目的 |
| ---------------------------- | ------- |
| **dmScale** | 指定缩放图像以进行打印的百分比。 |
| **dmCopies** | 指定要打印的份数。 |
| **dmColor** | 指定彩色打印机是否应打印颜色或单色。 |
| **dmOrientation** | 指定纸张的方向（纵向或横向）。 |

下一个表列出了几个 *仅* 由显示驱动程序使用的公共 DEVMODEW 成员：

|  仅由显示驱动程序使用 | 目的 |
| ----------------------------- | ------- |
| **dmBitsPerPel** | 指定显示设备的颜色分辨率（以每像素位数为单位）。 |
| **dmPelsWidth** | 指定可见设备图面的宽度（以像素为单位）。 |
| **dmPelsHeight** | 指定可见设备表面的高度（以像素为单位）。 |
| **dmDisplayFlags** | 指定显示模式-颜色与单色、交错与 noninterlaced。 |
| **dmDisplayFrequency** | 以赫兹为单位指定显示的刷新频率。 |

第三个表列出了打印机和显示器驱动程序使用的多个公共 DEVMODEW 成员：

| 打印机和显示器驱动程序使用| 目的 |
| ---------------------------------- | ------- |
| **dmDeviceName** | 对于 "显示"，指定显示驱动程序的 DLL。 对于 "打印机"，指定打印机的 "友好名称"。 |
| **dmFields** | 指定位标志，用于识别跟随其后的 DEVMODEW 成员。 例如，如果 **dmBitsPerPel** 成员包含有效数据，则会设置 DM_BITSPERPEL 标志。 |
| **dmSize** | 指定 DEVMODEW 结构的公共部分的大小（以字节为单位）。 |
| **dmDriverExtra** | 指定在公共结构成员后的专用驱动程序数据的字节数。 对于显示器驱动程序，此值通常为零。 |
