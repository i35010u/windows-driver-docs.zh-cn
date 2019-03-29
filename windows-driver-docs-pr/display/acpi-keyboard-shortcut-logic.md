---
title: ACPI 键盘快捷方式逻辑
description: ACPI 键盘快捷方式逻辑
ms.assetid: cd62380b-1393-403e-b0e6-c52f60c06936
keywords:
- ACPI 热键 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba92265c4f40d64e18cecef1f6f22d9f172fccd2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575945"
---
# <a name="acpi-keyboard-shortcut-logic"></a>ACPI 键盘快捷方式逻辑


从 Windows 7 开始，Ihv 实现基于 ACPI 的特定于 OEM 的键盘快捷方式。 操作系统不知道这些键盘快捷方式。 在 Windows 7 上 Oem 必须使用 CCD 数据库来存储和键盘快捷方式应用，以便操作系统和任何 OEM 应用程序能够相互识别。

以下函数的调用的行为已更改为 Windows 7 上运行的驱动程序：

<span id="DxgkDdiNotifyAcpiEvent_and_DxgkDdiRecommendFunctionalVidPn"></span><span id="dxgkddinotifyacpievent_and_dxgkddirecommendfunctionalvidpn"></span><span id="DXGKDDINOTIFYACPIEVENT_AND_DXGKDDIRECOMMENDFUNCTIONALVIDPN"></span>[*DxgkDdiNotifyAcpiEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff559695)并[ *DxgkDdiRecommendFunctionalVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559775)  
-   如果显示微型端口驱动程序接收到调用[ *DxgkDdiNotifyAcpiEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff559695)函数和 DXGK\_ACPI\_更改\_显示\_在中设置模式标志*AcpiFlags*参数，DMM 调用[ *DxgkDdiRecommendFunctionalVidPn* ](https://msdn.microsoft.com/library/windows/hardware/ff559775)函数来获取新 VidPN 并比较当前客户端 VidPN。 如果相同的两个 VidPNs 拓扑，DMM 不会修改新 VidPN。 否则为 DMM 从 VidPN，离开拓扑只是删除模式信息，并允许 CCD 数据库，以确定给定的拓扑的模式。 然后，DMM 设置基于新 VidPN 显示配置。

<span id="D3DKMTInvalidateActiveVidPn"></span><span id="d3dkmtinvalidateactivevidpn"></span><span id="D3DKMTINVALIDATEACTIVEVIDPN"></span>[**D3DKMTInvalidateActiveVidPn**](https://msdn.microsoft.com/library/windows/hardware/ff547023)  
-   此函数是在 Windows Vista 上受支持和更高版本进行显示微型端口驱动程序版本&lt;DXGKDDI\_界面\_版本\_WIN7。 函数行为等同于 Windows Vista 上的行为。

-   在 Windows 7 和更高版本的显示微型端口驱动程序版本不支持此函数&gt;= DXGKDDI\_界面\_版本\_WIN7。 如果调用，状态代码状态\_不\_返回受支持。

 

 





