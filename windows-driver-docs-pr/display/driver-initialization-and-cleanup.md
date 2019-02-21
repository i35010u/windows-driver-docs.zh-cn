---
title: 驱动程序初始化和清理
description: 驱动程序初始化和清理
ms.assetid: 57f22818-a298-4f9a-87a6-5ca4d97bf32b
keywords:
- 绘制 WDK GDI、 初始化、 说明
- 初始化的图形驱动程序 WDK Windows 2000 显示，请说明
- GDI WDK Windows 2000 显示、 初始化、 说明
- 图形驱动程序 WDK Windows 2000 显示，请初始化说明
- DrvEnableDriver
- 绘制 WDK GDI 清理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 997bef388a292c8e587f54a23eb74c4649f372f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520363"
---
# <a name="driver-initialization-and-cleanup"></a>驱动程序初始化和清理


## <span id="ddk_driver_initialization_and_cleanup_gg"></span><span id="DDK_DRIVER_INITIALIZATION_AND_CLEANUP_GG"></span>


它导出的设备驱动程序可以实现多个或多个函数，而仅[ **DrvEnableDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff556210)到 GDI。 该驱动程序公开其其他支持的函数，通过函数表。 GDI 对设备驱动程序，第一个调用是对**DrvEnableDriver**函数。 驱动程序中传入的此函数中将填充[ **DRVENABLEDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff556206)结构，使 GDI 能够确定哪些其他*DrvXxx*支持函数和位置它们是位于。 驱动程序提供 DRVENABLEDATA 中的以下信息：

-   **IDriverVersion**成员包含图形 DDI 版本特定的 Windows 操作系统版本的版本号。 *Winddi.h*标头定义以下常量：

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">Constant</th>
    <th align="left">操作系统版本</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>DDI_DRIVER_VERSION_NT4</p></td>
    <td align="left"><p>Windows NT 4.0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>DDI_DRIVER_VERSION_NT5</p></td>
    <td align="left"><p>Windows 2000</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>DDI_DRIVER_VERSION_NT5_01</p></td>
    <td align="left"><p>Windows XP</p></td>
    </tr>
    </tbody>
    </table>

     

有关如何使用这些常量的详细信息，请参阅[ **DRVENABLEDATA**](https://msdn.microsoft.com/library/windows/hardware/ff556206)。

-   **C**成员包含的数组中的 DRVFN 结构数。

-   **Pdrvfn**成员指向的数组[ **DRVFN** ](https://msdn.microsoft.com/library/windows/hardware/ff556221)列出了受支持的函数和及其索引的结构。

对于 GDI，若要调用的函数以外的驱动程序启用和禁用功能，该驱动程序必须提供函数的名称和位置向 GDI。

虽然[ **DrvEnableDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff556210)还可以执行一次性初始化、 信号量的分配，如驱动程序不应实际启用期间硬件**DrvEnableDriver**. 中的驱动程序应发生硬件初始化[ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)函数。 同样，驱动程序应启用中的面[ **DrvEnableSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff556214)函数。

GDI 调用[ **DrvDisableDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff556196)函数，以通知它是即将卸载该驱动程序。 此调用的响应，该驱动程序应释放所有资源和仍在此时由驱动程序分配的内存。

如果硬件需要重置，GDI 将调用的驱动程序[ **DrvAssertMode** ](https://msdn.microsoft.com/library/windows/hardware/ff556178)函数。

 

 





