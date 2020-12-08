---
title: Windows 8 中已更新的功能评分指令
description: 更新的功能分数指令是常规安装设置，该设置是所有遵循 Windows 显示驱动程序模型 (WDDM) 的 Windows 8 驱动程序所必需的。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94cd68f44f9f5900c55d8edb34917d9cbe2e3448
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802551"
---
# <a name="updated-feature-score-directive-in-windows-8"></a>Windows 8 中已更新的功能评分指令


更新的功能分数指令是常规安装设置，该设置是所有遵循 Windows 显示驱动程序模型 (WDDM) 的 Windows 8 驱动程序所必需的。

下表显示了适用于 Windows 8 的值。 关键更改是斜体。

**WDDM 版本的功能分数**

| 驱动程序型号                     | 功能分数                |
|----------------------------------|------------------------------|
| *Windows 8 WHQL*                 | *步进*                         |
| *Windows 8 预发行版驱动程序*   | *E3*                         |
| Windows 7 WHQL                   | E6                           |
| Windows 7 收件箱                  | EC                           |
| Windows Vista WHQL               | F6                           |
| Windows Vista 收件箱              | F8                           |
| *Microsoft 基本显示驱动程序* | *FB*                         |
| XDDM 第三方                 | *Windows 8) 不使用 FC (* |
| Windows Vista 中的 XDDM 收件箱      | FD *(在 Windows 8 中不使用)* |
| VGA                              | *在 Windows 8 中不使用 FE ()* |
| 默认或没有评分              | FF                           |
| 未签名驱动程序                 | 没有功能分数 = FF        |

 

每个操作系统版本引入了一个新的功能分数值。 对于 Windows 8，这是用于内置和预发行驱动程序的 *E3* ，适用于 WHQL 驱动程序的 *E0* 。 Windows 使用功能分数来确定存在多个可能的驱动程序时要安装的驱动程序。 选择了排名较高的功能分数的驱动程序。

由于在 Windows 8 上测试了内置驱动程序，并且现有的 Windows 7Windows 7 驱动程序尚未安装，因此，所有 Windows 8 内置驱动程序设备都具有比所有现有 Windows 7 驱动程序更高的排名。 这将导致替换现有 Windows 7 驱动程序的内置 Windows 8 驱动程序。 独立硬件供应商 (IHV) 如果满足以下条件，则可以将 E0 功能分数与 Windows 7 驱动程序结合使用：

-   已针对 Windows 8 对驱动程序进行了测试。
-   驱动程序提供的修补程序使其优于内置驱动程序。
-   驱动程序应在升级到 Windows 8 时保留。

 

 





