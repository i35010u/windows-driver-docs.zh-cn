---
title: 常规 x64 INF 信息
description: 常规 x64 INF 信息
ms.assetid: a1a96e8f-74d3-403d-994a-b21436d166d2
keywords:
- INF 文件 WDK 显示，64 位
- 64 位 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d6460ae99f513dcf006f491efa871019739276a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366333"
---
# <a name="general-x64-inf-information"></a>常规 x64 INF 信息


以下特定于 x64 的信息才可进行加载运行 64 位 Windows Vista 及更高版本的显示器驱动程序的 INF 文件：

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