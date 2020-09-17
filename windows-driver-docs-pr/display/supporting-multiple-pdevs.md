---
title: 支持多个 PDEV
description: 支持多个 PDEV
ms.assetid: e06fe2da-b677-4649-bf7a-09a8f2ddfc6b
keywords:
- 显示驱动程序 WDK Windows 2000，桌面管理
- 桌面管理 WDK Windows 2000 显示器
- 多 PDEVs WDK Windows 2000 显示器
- PDEV WDK Windows 2000 显示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddf4a40fb2e5bdb66a4a1809471d30951bacaf18
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715634"
---
# <a name="supporting-multiple-pdevs"></a>支持多个 PDEV


## <span id="ddk_supporting_multiple_pdevs_gg"></span><span id="DDK_SUPPORTING_MULTIPLE_PDEVS_GG"></span>


本部分说明在仍加载当前 PDEV 时，应用程序如何创建新的 PDEV。 控制面板的显示程序要求显示驱动程序支持其他 PDEVs，因为应用程序可以使用新桌面创建新的 PDEV。 具体来说，最终用户可以单击 "显示" 图标来对此类元素的更改运行测试，如屏幕的大小、颜色数和刷新速率。 显示程序会动态地创建一个新桌面，以测试显示的模式更改。

当用户单击显示图标请求模式更改时，GDI 会执行以下步骤。 以下步骤假定当前的驱动程序实例没有活动的 Direct3D、WNDOBJ 或 DRIVEROBJ 对象。

1.  暂时禁用当前 PDEV
    -   )  (旧的 PDEV 实例调用 [**DrvAssertMode**](/windows/win32/api/winddi/nf-winddi-drvassertmode) 。 如果微型端口驱动程序需要控制，则使用 **FALSE** 进行调用; 如果应使用 PDEV，则使用 **TRUE** 。

2.  如果新的 PDEV 实例需要，加载新的驱动程序 () 
    -   )  (新的驱动程序实例调用 [**DrvEnableDriver**](/windows/win32/api/winddi/nf-winddi-drvenabledriver) 。

3.  创建新的 PDEV
    -   )  (新的 PDEV 实例上调用 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 。
    -   )  (新的 PDEV 实例上调用 [**DrvCompletePDEV**](/windows/win32/api/winddi/nf-winddi-drvcompletepdev) 。
    -   )  (新的 PDEV 实例上调用 [**DrvEnableSurface**](/windows/win32/api/winddi/nf-winddi-drvenablesurface) 。

4.  如果 DirectDraw 由驱动程序) 挂钩，则获取 DirectDraw 信息 (。 仅当第一次调用成功时才调用 [**DrvGetDirectDrawInfo**](/windows/win32/api/winddi/nf-winddi-drvgetdirectdrawinfo) 。
    -   )  (新的 PDEV 实例上调用 *DrvGetDirectDrawInfo* 。
    -   )  (新的 PDEV 实例上调用 *DrvGetDirectDrawInfo* 。

5.  启用 DirectDraw (如果由驱动程序挂钩，并对 *DrvGetDirectDrawInfo* 的以前的调用成功) 。
    -   )  (新的 PDEV 实例上调用 [**DrvEnableDirectDraw**](/windows/win32/api/winddi/nf-winddi-drvenabledirectdraw) 。

6.  如果两个实例都使用相同的驱动程序，并且 DirectDraw 由驱动程序) 挂钩，则将旧的 PDEV 状态复制到新的 PDEV 实例 (。
    -   调用 [**DrvResetPDEV**](/windows/win32/api/winddi/nf-winddi-drvresetpdev)。

7.  通知每个驱动程序实例的新 HDEV 关联。 对 [**DrvCompletePDEV**](/windows/win32/api/winddi/nf-winddi-drvcompletepdev) 的第一次调用将通知新的驱动程序实例;第二次调用会通知旧的驱动程序实例。

    -   )  (新的 PDEV 实例上调用 *DrvCompletePDEV* 。
    -   )  (旧的 PDEV 实例调用 *DrvCompletePDEV* 。

    驱动程序应在需要 HDEV 的 GDI 的任何回调中使用新的 HDEV 值。

8.  如果由驱动程序挂钩，并且 DirectDraw 为活动) ，则禁用 DirectDraw (。
    -   )  (旧的 PDEV 实例调用 [**DrvDisableDirectDraw**](/windows/win32/api/winddi/nf-winddi-drvdisabledirectdraw) 。

9.  禁用图面。
    -   )  (旧的 PDEV 实例调用 [**DrvDisableSurface**](/windows/win32/api/winddi/nf-winddi-drvdisablesurface) 。

10. 禁用 PDEV。
    -   )  (旧的 PDEV 实例调用 [**DrvDisablePDEV**](/windows/win32/api/winddi/nf-winddi-drvdisablepdev) 。

在此示例中，当用户单击 "应用" 时，GDI 会暂时禁用当前 PDEV，然后创建与对话框中的显示模式选项匹配的第二个 PDEV。 用户在测试模式下的显示屏幕上查看位图后，第二个 PDEV 将被销毁，并且显示程序会还原桌面的原始 PDEV。 请注意，如果设置与硬件和驱动程序不兼容，则不能恢复回原始显示设置，系统将无法使用。

如果驱动程序的当前实例拥有 Direct3D、WNDOBJ 或 DRIVEROBJ 对象，则上一模式更改序列的驱动程序视图将按如下方式更改 (请注意，在 Windows 2000 和更高版本中，一旦初始化驱动程序，将始终启用 DirectDraw) ：

-   将延迟对所属驱动程序实例的析构。 具体而言，在模式发生更改时，第二次调用步骤7、步骤8和步骤9中的 [**DrvCompletePDEV**](/windows/win32/api/winddi/nf-winddi-drvcompletepdev) 不会出现。 因此，旧的驱动程序实例因调用 [**DrvAssertMode**](/windows/win32/api/winddi/nf-winddi-drvassertmode) (**FALSE**) 在步骤1中被禁用，并将保留，直到系统将模式更改回原始模式，或直到引用该实例的所有对象都被销毁。

-   如果系统在销毁引用对象之前恢复到原始模式，则原始驱动程序实例将为复活。 也就是说，不会执行步骤2到步骤5，并通过调用 *DrvAssertMode* (**TRUE**) 重新启用原始驱动程序实例 (参见步骤 1) 。

-   如果在销毁所有引用对象之前，系统不会恢复为原始模式，则在销毁最终的引用对象时，将销毁驱动程序实例。 也就是说，当最后一个引用对象被销毁时，将在步骤7、步骤8和步骤9中对 *DrvCompletePDEV* 进行第二次调用 (例如，当所有拥有的进程都) 终止时。

这意味着，可以随时调用 Direct3D 或 OpenGL 驱动程序来销毁非活动驱动程序实例。 即使驱动程序的另一个实例当前处于活动状态，或如果驱动程序处于全屏 MS-DOS 模式，或者其他驱动程序完全 (（例如 VGA 驱动程序) ），也可以调用这些驱动程序。 因此， [**DrvDisableDirectDraw**](/windows/win32/api/winddi/nf-winddi-drvdisabledirectdraw)、 [**DrvDisableSurface**](/windows/win32/api/winddi/nf-winddi-drvdisablesurface)和 [**DrvDisablePDEV**](/windows/win32/api/winddi/nf-winddi-drvdisablepdev) 例程 (查看驱动程序的步骤 8-10) 不会假定设备处于图形模式并且它们拥有独占访问权限。 通常情况下，驱动程序不应在其 *DrvDisableXxx* 例程中操作其视频硬件，除非他们知道其实例当前处于活动状态 (通过记住最后一次 [**DrvAssertMode**](/windows/win32/api/winddi/nf-winddi-drvassertmode) 调用中的状态) 。

**注意**   PDEV 专用于驱动程序，包含表示关联的物理设备的所有信息和数据。 若要创建多个 PDEVs，图形驱动程序必须满足以下两个要求：
1.  驱动程序不得使用全局变量，而不能取消引用 PDEV 结构的成员。 如果使用全局变量，则在创建新的 PDEV 或还原新的时，它们可能包含或指向随机数据。 所有状态信息都必须保存在 PDEV 中。 PDEV 始终传递到任何图形操作，因此用于获取或设置全局数据。

2.  必须在图形驱动程序中实现 [**DrvDisableSurface**](/windows/win32/api/winddi/nf-winddi-drvdisablesurface)、 [**DrvDisablePDEV**](/windows/win32/api/winddi/nf-winddi-drvdisablepdev)和 [**DrvDisableDriver**](/windows/win32/api/winddi/nf-winddi-drvdisabledriver) 例程，以便应用程序可以创建和销毁其他 PDEVs，在某些情况下会加载多个驱动程序。

 

**注意**   如果驱动程序的版本号为1.0，则 GDI 不会调用驱动程序来创建第二个 PDEV。 在 [**DRVENABLEDATA**](/windows/win32/api/winddi/ns-winddi-tagdrvenabledata)中返回驱动程序的版本号。

 

**注意**   有时，显示程序的测试位图将使用与当前加载的驱动程序不同的驱动程序来显示。 例如，如果系统在带有 VGA 驱动程序的16色模式下运行，并使用 VGA64K 显示驱动程序测试64K 彩色模式，则在测试完成后，将动态加载 VGA64K 驱动程序并将其卸载。

 

 

