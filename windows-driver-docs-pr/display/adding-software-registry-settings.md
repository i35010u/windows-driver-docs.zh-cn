---
title: 添加软件注册表设置
description: 添加软件注册表设置
keywords:
- INF 文件 WDK 显示，软件注册表设置
- 软件注册表设置 WDK 显示
- 注册表 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 347fffe043b25a04494c1b777789c8dcbf111945
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810537"
---
# <a name="adding-software-registry-settings"></a>添加软件注册表设置


INF 文件必须将所有软件注册表设置添加到即插即用 (PnP) 软件密钥，如以下示例中所示：

```inf
[Xxx.Mfg]
"RADEON 8500/RADEON 8500LE (R200 LDDM)" = R200_R200, PCI\VEN_1002&DEV_514c&SUBSYS_003a1002

[R200_R200]
Include=msdv.inf
CopyFiles=R200.Miniport, R200.Display
AddReg = R200_SoftwareDeviceSettings
AddReg = R200_R200_SoftwareDeviceSettings
DelReg = R200_RemoveDeviceSettings 
```

 

 





