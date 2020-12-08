---
title: 返回状态
description: 返回状态
keywords:
- status 值 WDK 文件系统
- 成功状态值 WDK 文件系统
- 返回状态 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af75bada9637a78fdb8e2cfd5e620e553d7bb6a4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816245"
---
# <a name="returning-status"></a>返回状态


## <span id="ddk_returning_status_if"></span><span id="DDK_RETURNING_STATUS_IF"></span>


文件系统筛选器驱动程序的 **DriverEntry** 例程通常返回状态 " \_ 成功"。 但是，如果驱动程序初始化失败， **DriverEntry** 例程应返回相应的错误状态值。

如果 **DriverEntry** 例程返回的状态值不是成功状态值，系统将通过卸载驱动程序来做出响应。 出于此原因，在返回不是 "成功" 状态值的状态值之前， **DriverEntry** 例程必须始终释放为系统资源分配的任何内存，如设备对象。

 

 




