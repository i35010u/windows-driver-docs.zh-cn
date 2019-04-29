---
title: Windows 8 中已更新的功能评分指令
description: 更新的功能分数指令是以遵循 Windows 显示器驱动程序模型 (WDDM) 的所有 Windows 8 驱动程序所需的常规安装设置。
ms.assetid: E50E132A-DEC8-42F4-AAF8-05F658990CF5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f23be96576ac2d2328f7a8e6cf45a7d83e56607e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389804"
---
# <a name="updated-feature-score-directive-in-windows-8"></a>Windows 8 中已更新的功能评分指令


更新的功能分数指令是以遵循 Windows 显示器驱动程序模型 (WDDM) 的所有 Windows 8 驱动程序所需的常规安装设置。

此表显示适用于 Windows 8 的值。 密钥更改为斜体。

**WDDM 版本的特征分数**

| 驱动程序模型                     | 特征评分                |
|----------------------------------|------------------------------|
| *Windows 8 WHQL*                 | *E0*                         |
| *预发行版的 Windows 8 驱动程序*   | *E3*                         |
| Windows 7 WHQL                   | E6                           |
| Windows 7 收件箱                  | EC                           |
| Windows Vista WHQL               | F6                           |
| Windows Vista 收件箱              | F8                           |
| *Microsoft 基本显示驱动程序* | *FB*                         |
| XDDM 第三方                 | FC *（未在 Windows 8 中使用）* |
| Windows Vista 中的 XDDM 收件箱      | FD *（未在 Windows 8 中使用）* |
| VGA                              | FE *（未在 Windows 8 中使用）* |
| 默认值或任何得分              | FF                           |
| 未签名驱动程序                 | 任何功能得分 = FF        |

 

每个操作系统版本引入了新功能得分值。 这是针对 Windows 8 *E3*中框和预发布版本的驱动程序，并*E0* WHQL 驱动程序。 特征评分是 Windows 用于确定要安装多个可能的驱动程序存在时的驱动程序。 选择的驱动程序有较高的排名的功能得分。

所有 Windows 8 中现成驱动程序设备都具有较高的排名的功能得分比所有现有的 Windows 7 驱动程序，因为现成驱动程序测试在 Windows 8 中，并且现有 Windows 7Windows 7 驱动程序尚未。 这会导致现成 Windows 8 驱动程序以替换现有的 Windows 7 驱动程序。 如果满足下列条件时，独立硬件供应商 (IHV) 可以通过 Windows 7 驱动程序使用 E0 特征评分：

-   已针对 Windows 8 中测试驱动程序。
-   该驱动程序有使其优于现成驱动程序的修补程序。
-   该驱动程序旨在保留在升级到 Windows 8 上。

 

 





