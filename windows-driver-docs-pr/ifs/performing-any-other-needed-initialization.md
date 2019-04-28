---
title: 执行任何其他必需的初始化
description: 执行任何其他必需的初始化
ms.assetid: 781f241f-fb12-460e-b093-ffa916aae495
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e93262dd653ad7fd17f260ff38f75a61135dd745
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352772"
---
# <a name="performing-any-other-needed-initialization"></a>执行任何其他必需的初始化


## <span id="ddk_performing_any_other_needed_initialization_if"></span><span id="DDK_PERFORMING_ANY_OTHER_NEEDED_INITIALIZATION_IF"></span>


注册 IRP 和快速 I/O 之后调度例程，文件系统筛选器驱动程序**DriverEntry**例程可以根据需要初始化其他全局驱动程序变量和数据结构。

 

 




