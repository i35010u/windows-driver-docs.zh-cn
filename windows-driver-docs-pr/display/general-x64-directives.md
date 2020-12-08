---
title: 常规 x64 指令
description: 本主题介绍适当修饰用于64位 Windows 的 INF 所需的更改。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0b70f49c59ce52b61607f9a49dfd9a229da0897
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803929"
---
# <a name="general-x64-directives"></a>常规 x64 指令


本主题介绍适当修饰用于64位 Windows 的 INF 所需的更改。

例如：

``` syntax
[DestinationDirs]
DefaultDestDir  = 11
R200.Miniport   = 12  ; drivers
R200.Display    = 11  ; system32
R200.DispWow  = 10, SysWow64

[Manufacturer]
%ATI% = ATI.Mfg, NTamd64

[ATI.Mfg.NTamd64]

[R200_RV200]
FeatureScore=F8
CopyFiles=R200.Miniport, R200.Display, R200.DispWow
AddReg = R200_SoftwareDeviceSettings
AddReg = R200_RV200_SoftwareDeviceSettings
DelReg = R200_RemoveDeviceSettings

; File sections
;

[r200.Miniport]
r200.sys

[r200.Display]
r200umd.dll,,,0x00004000             ; COPYFLG_IN_USE_TRY_RENAME

[R200.DispWow]
r2umd32.dll,,,0x00004000             ; COPYFLG_IN_USE_TRY_RENAME
```

 

 





