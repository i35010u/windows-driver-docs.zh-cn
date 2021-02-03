---
title: 筛选上下文最佳实践
description: 最佳实践
keywords:
- 上下文 WDK 文件系统微筛选器，最佳实践
ms.date: 01/20/2021
ms.localizationpriority: medium
ms.openlocfilehash: 181104bb0153955d4b448a713eebd865282a9df6
ms.sourcegitcommit: 204ed37ede1cd462ef6f6c9211a223fd304da4a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "99502048"
---
# <a name="filter-context-best-practices"></a>筛选上下文最佳实践

如果微筛选器驱动程序只为每个卷创建一个微筛选器驱动程序实例，则应使用实例上下文而不是卷上下文来提高性能。

还可以通过在其流或流句柄上下文内存储一个指向微筛选器驱动程序实例上下文的指针来提高性能。
