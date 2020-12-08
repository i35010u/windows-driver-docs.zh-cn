---
title: 常规 x64 INF 信息
description: 常规 x64 INF 信息
keywords:
- INF 文件 WDK 显示，64位
- 64位 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2648e7b38323ab033229714cdbf6a9a371345e23
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803925"
---
# <a name="general-x64-inf-information"></a>常规 x64 INF 信息


对于加载在64位 Windows Vista 和更高版本上运行的显示驱动程序的 INF 文件，需要以下 x64 特定信息：

```inf
[DestinationDirs]
DefaultDestDir  = 11
R200.Miniport   = 12  ; drivers
R200.Display    = 11  ; system32
R200.DispWow  = 10, SysWow64 ; x64-specific

[Manufacturer]
%ATI% = ATI.Mfg, NTamd64 ; Ntamd64 is x64-specific

[ATI.Mfg.NTamd64] ; Ntamd64 is x64-specific

[R200_RV200]
FeatureScore=F8
CopyFiles=R200.Miniport, R200.Display, R200.DispWow ; R200.DispWow is x64-specific
AddReg = R200_SoftwareDeviceSettings
AddReg = R200_RV200_SoftwareDeviceSettings
DelReg = R200_RemoveDeviceSettings

; File sections
;

[r200.Miniport]
r200.sys

[r200.Display]
r200umd.dll,,,0x00004000  ; COPYFLG_IN_USE_TRY_RENAME

; The following [R200.DispWow] section is x64-specific

[R200.DispWow]
r2umd32.dll,,,0x00004000  ; COPYFLG_IN_USE_TRY_RENAME
```
