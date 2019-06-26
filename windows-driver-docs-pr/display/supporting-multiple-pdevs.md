---
title: 支持多个 PDEV
description: 支持多个 PDEV
ms.assetid: e06fe2da-b677-4649-bf7a-09a8f2ddfc6b
keywords:
- 显示驱动程序 WDK Windows 2000 中，桌面管理
- 桌面管理 WDK Windows 2000 显示
- 多个 PDEVs WDK Windows 2000 显示
- PDEV WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecc155ef6ffd804c01c7a9aecce9e36d3b8c93b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380543"
---
# <a name="supporting-multiple-pdevs"></a>支持多个 PDEV


## <span id="ddk_supporting_multiple_pdevs_gg"></span><span id="DDK_SUPPORTING_MULTIPLE_PDEVS_GG"></span>


本部分介绍如何应用程序可以创建新 PDEV 时当前 PDEV 仍处于加载状态。 控制面板中的显示计划要求显示驱动程序支持启用其他 PDEVs，因为它是应用程序可以使用新的桌面中创建新 PDEV。 具体而言，最终用户可以单击显示图标以运行测试上更改到大小、 颜色数与此类元素，并刷新屏幕的频率。 显示程序创建新的桌面动态，若要测试的显示模式更改。

当用户单击显示图标，以请求模式更改时，GDI 将执行以下步骤。 这些步骤假定没有活动的 Direct3D、 WNDOBJ 或 DRIVEROBJ 对象所拥有的当前驱动程序实例。

1.  临时禁用当前 PDEV
    -   调用[ **DrvAssertMode** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode) （旧 PDEV 实例）。 调用了使用**FALSE**如果微型端口驱动程序将负责控制，且**TRUE**如果应使用 PDEV。

2.  加载新的驱动程序 （如果所需的新 PDEV 实例）
    -   调用[ **DrvEnableDriver** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver) （新驱动程序实例）。

3.  创建新 PDEV
    -   调用[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev) （新 PDEV 实例）。
    -   调用[ **DrvCompletePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev) （新 PDEV 实例）。
    -   调用[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface) （新 PDEV 实例）。

4.  获取 DirectDraw 信息 （如果 DirectDraw 连接驱动程序）。 第二次调用到[ **DrvGetDirectDrawInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)仅当第一次调用成功进行。
    -   调用*DrvGetDirectDrawInfo* （新 PDEV 实例）。
    -   调用*DrvGetDirectDrawInfo* （新 PDEV 实例）。

5.  启用 DirectDraw (如果驱动程序和对上一个调用挂钩*DrvGetDirectDrawInfo*成功)。
    -   调用[ **DrvEnableDirectDraw** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledirectdraw) （新 PDEV 实例）。

6.  将旧 PDEV 状态复制到新 PDEV 实例 （如果这两个实例都使用相同的驱动程序，并由驱动程序挂接 DirectDraw）。
    -   调用[ **DrvResetPDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvresetpdev)。

7.  通知其新 HDEV 关联的每个驱动程序实例。 首次调用[ **DrvCompletePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)通知新的驱动程序实例; 第二次调用通知旧驱动程序实例。

    -   调用*DrvCompletePDEV* （新 PDEV 实例）。
    -   调用*DrvCompletePDEV* （旧 PDEV 实例）。

    驱动程序应使用新的 HDEV 值需要 HDEV 任何回调到 GDI 中。

8.  禁用 DirectDraw （如果驱动程序和 DirectDraw 连接处于活动状态）。
    -   调用[ **DrvDisableDirectDraw** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledirectdraw) （旧 PDEV 实例）。

9.  禁用图面。
    -   调用[ **DrvDisableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface) （旧 PDEV 实例）。

10. 禁用 PDEV。
    -   调用[ **DrvDisablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev) （旧 PDEV 实例）。

在此示例中，GDI 暂时禁用当前 PDEV 当用户单击应用，然后创建第二个 PDEV 相匹配的对话框中的显示模式选项。 用户在测试模式下显示屏幕上查看位图后，第二个 PDEV 销毁并显示程序将还原原始 PDEV 适用于桌面。 请注意不能还原为原始显示设置，系统会变为不可用，如果设置了与硬件和驱动程序不兼容。

如果该驱动程序的当前实例拥有 Direct3D、 WNDOBJ 或 DRIVEROBJ 对象，以前的模式下更改序列的驱动程序的视图发生更改，如下所示 （请注意，在 Windows 2000 及更高版本，DirectDraw 始终启用后初始化该驱动程序）：

-   析构的所属的驱动程序实例将被延迟。 具体而言，到第二次调用[ **DrvCompletePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)第 7 步，在步骤 8，和步骤 9 将不会出现在模式更改的时间。 因此，旧的驱动程序实例禁用对的调用由于[ **DrvAssertMode**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)(**FALSE**) 中的步骤 1，并保留，直到任一系统将执行一种模式改回为原始的模式，或直到引用实例的所有对象被都销毁。

-   如果引用的对象被销毁之前，系统会恢复到原始模式下，将重新恢复原始的驱动程序实例。 也就是说，步骤 2 到 5 不会发生，并且原始的驱动程序实例将重新启用通过调用*DrvAssertMode*(**TRUE**) （请参阅步骤 1）。

-   如果系统不会恢复回原始模式在所有引用之前对象将被破坏，则驱动程序实例将销毁的最后一个引用对象时销毁。 第二次调用，即*DrvCompletePDEV*第 7 步，在步骤 8，并在最后一个引用对象被销毁 （例如，当所有拥有的进程将终止） 时间发生步骤 9。

这是可以调用 Direct3D 或 OpenGL 的驱动程序以在任何时候销毁处于非活动状态的驱动程序实例。 可以调用这些驱动程序，即使该驱动程序的另一个实例当前处于活动状态，或该驱动程序是在全屏幕 MS-DOS 模式下，或另一个驱动程序拥有完全 （如 VGA 驱动程序） 的硬件。 因此， [ **DrvDisableDirectDraw**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledirectdraw)， [ **DrvDisableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)，并[ **DrvDisablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)例程 （请参见步骤 8-10） 的驱动程序不能假定设备已在图形模式下并且他们自己拥有独占访问权限。 作为一般规则，驱动程序不应控制其视频硬件中的其*DrvDisableXxx*例程除非他们知道其实例当前处于活动状态 (从上一个记住状态[ **DrvAssertMode** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)调用)。

**请注意**   PDEV 是私有的驱动程序和包含的所有信息和表示关联的物理设备的数据。 若要创建多个 PDEVs，图形驱动程序必须满足这两个以下要求：
1.  驱动程序必须使用全局变量而不是取消引用 PDEV 结构的成员。 如果未使用全局变量，也可能包含或指向随机数据时创建新 PDEV，或还原的旧其中一个。 必须将所有状态信息都保存在 PDEV。 PDEV 始终传递给任何图形操作，因此用于获取或设置全局数据。

2.  [ **DrvDisableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)， [ **DrvDisablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)，并[ **DrvDisableDriver**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)例程必须实现图形驱动程序中，以便应用程序可以创建和销毁其他 PDEVs，并在某些情况下加载多个驱动程序。

 

**请注意**  如果驱动程序的版本号为 1.0，GDI 将不会调用要创建第二个 PDEV 的驱动程序。 中返回该驱动程序的版本号[ **DRVENABLEDATA**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)。

 

**请注意**  有时，显示程序的测试将不显示位图使用比当前加载的驱动程序的不同驱动程序。 例如，如果系统正在 16 色模式下使用 VGA 驱动程序和测试与 VGA64K 64k 颜色模式显示驱动程序，VGA64K 驱动程序会动态加载和卸载测试完成后。

 

 

 





