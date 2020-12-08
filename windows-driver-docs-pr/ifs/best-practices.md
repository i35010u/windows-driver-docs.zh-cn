---
title: 最佳实践
description: 最佳方案
keywords:
- 上下文 WDK 文件系统微筛选器，最佳实践
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 434c85df5b2f34e245edcb6db2abc18267ccfd40
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824139"
---
# <a name="best-practices"></a>最佳方案


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


如果微筛选器驱动程序只为每个卷创建一个微筛选器驱动程序实例，则它应使用实例上下文而不是卷上下文来提高性能。

微筛选器驱动程序还可以通过将指向微筛选器驱动程序实例上下文的指针存储在其流或流句柄上下文中来提高性能。

 

 




