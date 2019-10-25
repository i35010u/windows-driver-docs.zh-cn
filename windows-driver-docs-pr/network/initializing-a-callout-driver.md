---
title: 初始化标注驱动程序
description: 初始化标注驱动程序
ms.assetid: c9fbc3d9-fcb9-4087-a3d9-d97c64711305
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95829f01fecd01f92967e301510f8d3e8d73fc0d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824605"
---
# <a name="initializing-a-callout-driver"></a>初始化标注驱动程序


标注驱动程序在其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数内初始化自身。 主要的初始化任务如下所示：

-   [指定 Unload 函数](specifying-an-unload-function.md)

-   [创建设备对象](creating-a-device-object.md)

-   [向筛选器引擎注册标注](registering-callouts-with-the-filter-engine.md)

 

 





