---
title: 初始化标注驱动程序
description: 初始化标注驱动程序
ms.assetid: c9fbc3d9-fcb9-4087-a3d9-d97c64711305
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1838df6b009087791ad9811ecdd702793b422412
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371849"
---
# <a name="initializing-a-callout-driver"></a>初始化标注驱动程序


标注驱动程序初始化单独存在于其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)函数。 主要的初始化任务如下所示：

-   [指定卸载函数](specifying-an-unload-function.md)

-   [创建设备对象](creating-a-device-object.md)

-   [使用筛选器引擎注册标注](registering-callouts-with-the-filter-engine.md)

 

 





