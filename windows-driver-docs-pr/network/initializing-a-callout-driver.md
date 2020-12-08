---
title: 初始化标注驱动程序
description: 初始化标注驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79b95be8b5d0c64d1198e4dbfa825d7717da4564
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786149"
---
# <a name="initializing-a-callout-driver"></a>初始化标注驱动程序


标注驱动程序在其 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 函数内初始化自身。 主要的初始化任务如下所示：

-   [指定卸载函数](specifying-an-unload-function.md)

-   [创建设备对象](creating-a-device-object.md)

-   [将标注注册到筛选器引擎](registering-callouts-with-the-filter-engine.md)

 

