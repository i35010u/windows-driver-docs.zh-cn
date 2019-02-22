---
title: 返回状态
description: 返回状态
ms.assetid: fd490517-f4c5-4e20-9eac-6a9ac7d04992
keywords:
- 状态值 WDK 文件系统
- 成功状态的值 WDK 文件系统
- 返回状态 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b42dfacd2daedcf2011e06d9eb3f90fa08ab6d36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534407"
---
# <a name="returning-status"></a>返回状态


## <span id="ddk_returning_status_if"></span><span id="DDK_RETURNING_STATUS_IF"></span>


文件系统筛选器驱动程序的**DriverEntry**例程通常将返回状态\_成功。 但是，如果驱动程序初始化失败，则**DriverEntry**例程应返回相应的错误状态值。

如果**DriverEntry**例程将返回不是一个成功的状态值的状态值，系统就会卸载该驱动程序。 出于此原因， **DriverEntry**例程必须始终释放已分配的系统资源，例如设备的对象，然后再返回一个状态值不是成功状态的值，该值的任何内存。

 

 




