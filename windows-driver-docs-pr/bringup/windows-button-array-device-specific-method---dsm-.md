---
title: Windows 按钮数组的特定于设备的方法 (_DSM)
description: 若要支持的 Windows 按钮用户界面 (UI) 的发展，Windows 在本文中定义函数所述的 Windows 按钮数组设备特定于设备的方法 (_DSM)。
ms.assetid: B79ED0F9-B46A-4915-8FF3-5CF3D2E0E945
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fdfa6c35d0cfc715401c7b89f42f6c9c35d8466
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338093"
---
# <a name="windows-button-array-device-specific-method-dsm"></a>Windows 按钮数组特定于设备的方法 (\_DSM)


若要支持的 Windows 按钮用户界面 (UI) 的发展，Windows 定义了特定于设备的方法 (\_DSM) 的 Windows 按钮数组设备与本文中所述的函数。

## <a name="function-1-power-button-properties"></a>函数 1:电源按钮属性


\_DSM 控件方法参数的电源按钮属性函数如下所示：

### <a name="arguments"></a>参数

-   **Arg0:** UUID = dfbcf3c5-e7a5-44e6-9c1f-29c76f6e059c
-   **Arg1:** 修订 ID = 0
-   **Arg2:** 函数索引 = 1
-   **Arg3:**（未使用） 的空包

### <a name="return"></a>返回

具有以下位域定义一个整数 (DWORD):

-   Bits 31 到 33:保留 （必须是 0）。
-   2 位：如果检测到这两个按和发布事件，并向操作系统报告这些事件配置的电源按钮应设置此位为 1。 否则，此位应为 0。
-   1 位：此位应设置为 1，如果电源按钮被绑定到构成中断控制器 (GPIO 或其他) 的支持级别检测。 否则，此位应为 0。
-   位 0:如果该平台支持 ACPI 电源按钮的重写时间为 10 秒或更高版本应设置此位为 1。 否则，此位应为 0。

**请注意**  函数索引为 0 的每个\_DSM 是返回集支持的函数的索引，并始终是必需的查询函数。 有关详细信息，请参阅部分 9.14.1，"\_DSM （设备特定的方法）"，在[ACPI 5.0 规范](https://www.uefi.org/specifications)。

 

 

 




