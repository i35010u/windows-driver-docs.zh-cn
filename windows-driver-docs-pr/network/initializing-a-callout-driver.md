---
title: 初始化标注驱动程序
description: 初始化标注驱动程序
ms.assetid: c9fbc3d9-fcb9-4087-a3d9-d97c64711305
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1af9404329ebc88fc117cceea4726178232934b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210731"
---
# <a name="initializing-a-callout-driver"></a>初始化标注驱动程序


标注驱动程序在其 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 函数内初始化自身。 主要的初始化任务如下所示：

-   [指定卸载函数](specifying-an-unload-function.md)

-   [创建设备对象](creating-a-device-object.md)

-   [将标注注册到筛选器引擎](registering-callouts-with-the-filter-engine.md)

 

