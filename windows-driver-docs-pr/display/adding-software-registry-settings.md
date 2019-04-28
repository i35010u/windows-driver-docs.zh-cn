---
title: 添加软件注册表设置
description: 添加软件注册表设置
ms.assetid: 96c7fc9e-885c-43ec-973a-6e6d984fe7d0
keywords:
- INF 文件 WDK 显示、 软件注册表设置
- 软件注册表设置 WDK 显示
- 注册表 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f02512d274d0cffe5d84a30ec396253977b88df8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341615"
---
# <a name="adding-software-registry-settings"></a>添加软件注册表设置


INF 文件必须 (PnP) 插到软件密钥，如下面的示例中所示添加所有软件注册表设置：

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

 

 





