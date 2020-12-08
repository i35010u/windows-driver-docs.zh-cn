---
title: WDDM 1.2 驱动程序实施
description: Microsoft DirectX graphics 内核子系统 (Dxgkrnl) 的验证是从 Windows 8 开始强制执行的，以确定 WDDM 1.2 驱动程序是否支持必需的 Windows 显示驱动程序模型 (WDDM) 1.2 功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3004122192b4e38d1607220e7a9465740fe66483
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786361"
---
# <a name="wddm-12-driver-enforcement"></a>WDDM 1.2 驱动程序实施


Microsoft DirectX graphics 内核子系统 (Dxgkrnl) 的验证是从 Windows 8 开始强制执行的，以确定 WDDM 1.2 驱动程序是否支持必需的 Windows 显示驱动程序模型 (WDDM) 1.2 功能。

WDDM 1.2 具有强制功能和可选功能。 驱动程序必须将所有必需的功能 cap 设置为以 WDDM 1.2 驱动程序的形式声明自身，同时驱动程序可以实现任何组合 (或无可选功能) 。 非 WDDM 1.2 驱动程序必须报告 WDDM 1.2 的任何功能。

## <a name="span-iduser_experience_when_a_driver_fails_the_dxgkrnl_validationspanspan-iduser_experience_when_a_driver_fails_the_dxgkrnl_validationspanspan-iduser_experience_when_a_driver_fails_the_dxgkrnl_validationspanuser-experience-when-a-driver-fails-the-dxgkrnl-validation"></a><span id="User_experience_when_a_driver_fails_the_Dxgkrnl_validation"></span><span id="user_experience_when_a_driver_fails_the_dxgkrnl_validation"></span><span id="USER_EXPERIENCE_WHEN_A_DRIVER_FAILS_THE_DXGKRNL_VALIDATION"></span>驱动程序在 Dxgkrnl 验证失败时的用户体验


如果驱动程序错误地将自身声明为 WDDM 1.2 或仅实现了某些必需的功能，则它将无法创建适配器，并且系统将回退到 Microsoft 基本显示器驱动程序 (MSBDD) 。

 

 





