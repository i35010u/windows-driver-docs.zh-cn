---
title: 设置驱动程序控制标志
description: 设置驱动程序控制标志
ms.assetid: cca51b9c-ce37-4efb-ab42-8eb62b25eb21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6465e13c11f5f75b2b0fb1cb5fce098849e510b6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365558"
---
# <a name="setting-the-driver-control-flags"></a>设置驱动程序控制标志


**ExcludeFromSelect**指令所需的所有驱动程序，除[镜像驱动程序](mirror-drivers.md)，编写为 Windows 显示器驱动程序模型 (WDDM)。

下面的示例演示如何添加**ExcludeFromSelect**指令**ControlFlags** INF 文件的部分：

```inf
[ControlFlags]
ExcludeFromSelect=*
```

有关驱动程序控制标志的详细信息，请参阅[ **INF ControlFlags 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-controlflags-section)。

 

 





