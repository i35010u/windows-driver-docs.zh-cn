---
title: 最佳方案
description: 最佳方案
ms.assetid: c01b3fd9-7f4e-4d1a-a726-b31b0eebf094
keywords:
- 上下文 WDK 文件系统微筛选器，最佳做法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34a915656bd3f24a05af4553aaa30818ba84f482
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525866"
---
# <a name="best-practices"></a>最佳方案


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


如果微筛选器驱动程序创建只有一个微筛选器驱动程序实例，每个卷，它应使用更好的性能实例上下文而不是卷的上下文。

微筛选器驱动程序还可以通过存储指向其流内的微筛选器驱动程序实例上下文的指针来提高性能或流句柄上下文。

 

 




