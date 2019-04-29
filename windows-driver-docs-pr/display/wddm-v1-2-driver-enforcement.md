---
title: WDDM 1.2 驱动程序实施
description: 从 Windows 8，以确定是否通过 WDDM 1.2 驱动程序支持强制 Windows 显示驱动程序模型 (WDDM) 1.2 功能开始强制执行由 Microsoft DirectX 图形内核子系统 (Dxgkrnl) 验证。
ms.assetid: DF0C6F50-CC68-4002-9ED3-F42EA24D24B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c596a2f25f46e1d35d85a80a8152cd18566548e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391189"
---
# <a name="wddm-12-driver-enforcement"></a>WDDM 1.2 驱动程序实施


从 Windows 8，以确定是否通过 WDDM 1.2 驱动程序支持强制 Windows 显示驱动程序模型 (WDDM) 1.2 功能开始强制执行由 Microsoft DirectX 图形内核子系统 (Dxgkrnl) 验证。

WDDM 1.2 具有必需和可选功能。 该驱动程序必须设置所有必需功能 caps 声明本身作为 WDDM 1.2 驱动程序，而该驱动程序可以实现的可选功能的任意组合 （或无）。 WDDM 1.2 驱动程序必须报告的任何 WDDM 1.2 功能。

## <a name="span-iduserexperiencewhenadriverfailsthedxgkrnlvalidationspanspan-iduserexperiencewhenadriverfailsthedxgkrnlvalidationspanspan-iduserexperiencewhenadriverfailsthedxgkrnlvalidationspanuser-experience-when-a-driver-fails-the-dxgkrnl-validation"></a><span id="User_experience_when_a_driver_fails_the_Dxgkrnl_validation"></span><span id="user_experience_when_a_driver_fails_the_dxgkrnl_validation"></span><span id="USER_EXPERIENCE_WHEN_A_DRIVER_FAILS_THE_DXGKRNL_VALIDATION"></span>用户体验驱动程序未能通过 Dxgkrnl 验证时


如果驱动程序已错误地将自身声明为 WDDM 1.2 或已实现只有某些必需的功能，然后它将无法创建适配器，并且系统将回退到 Microsoft 基本显示驱动程序 (MSBDD)。

 

 





