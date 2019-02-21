---
title: 驱动程序验证程序管理器 (Windows 2000)
description: 驱动程序验证程序管理器 (Windows 2000)
ms.assetid: d1266d2d-2388-472d-a1c4-875ed24913d4
keywords:
- 驱动程序验证程序管理器
- 验证程序实用工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f7c17054c0b4065eaa72cc4f2c889217a6127d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521605"
---
# <a name="driver-verifier-manager-windows-2000"></a>驱动程序验证程序管理器 (Windows 2000)


## <span id="ddk_driver_verifier_manager_windows_2000__tools"></span><span id="DDK_DRIVER_VERIFIER_MANAGER_WINDOWS_2000__TOOLS"></span>


Windows 2000 版本的驱动程序验证程序管理器具有五个单独的面板：

1.  **驱动程序状态**屏幕将显示该驱动程序加载和进行验证，以及哪些 Driver Verifier 选项处于活动状态。 请参阅[查看驱动程序验证器设置](viewing-driver-verifier-settings.md)有关详细信息。

2.  **全局计数器**屏幕将显示与 Driver Verifier 的操作相关的统计信息。 尽管某些统计信息相关的某些驱动程序验证程序选项，将显示这些统计信息，无论哪个选项处于活动状态。 请参阅[监视全局计数器](monitoring-global-counters.md)有关详细信息。

3.  **池跟踪**屏幕将显示有关池分配的信息。 请参阅[监视各个计数器](monitoring-individual-counters.md)有关详细信息。

4.  **设置**屏幕用于激活和配置驱动程序验证程序的操作。 在下一次启动后，在此屏幕中所做的更改才会生效。 请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)并[选择驱动程序，以验证](selecting-drivers-to-be-verified.md)有关详细信息。

5.  **易失性设置**屏幕用于更改驱动程序验证程序的易失性操作。 在此屏幕中所做的更改会立即生效。 请参阅[使用易失性设置](using-volatile-settings.md)有关详细信息。

具有多个屏幕**刷新频率**对它们的部分。 这用于控制该屏幕上显示的信息更新的频率。 **低**，**中等**，和**高**指示驱动程序验证程序来分别每隔 1、 5 或 10 秒钟，刷新屏幕。 **手动**禁用自动更新。 **立即刷新**按钮会导致要立即刷新屏幕。

若要退出驱动程序验证程序管理器，请使用**退出**按钮。 如果进行了任何更改并且未按相应**应用**按钮，系统将要求你是否希望保存所做的更改。

 

 





