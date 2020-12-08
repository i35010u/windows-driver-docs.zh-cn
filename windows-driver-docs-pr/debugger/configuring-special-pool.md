---
title: 配置特殊池
description: 配置特殊池
keywords:
- GFlags，配置内核特殊池
- 内核特殊池
- 特殊池
- 池标记和特殊池
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc2d4437a71afd5a164eeb59730f7223a70c5559
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818641"
---
# <a name="configuring-special-pool"></a>配置特殊池


## <span id="ddk_configuring_kernel_special_pool_dtools"></span><span id="DDK_CONFIGURING_KERNEL_SPECIAL_POOL_DTOOLS"></span>


当使用指定的池标记分配内存或在指定的大小范围内时，Gflags *特殊池* 功能可指示 Windows 请求从保留内存池中分配内存。

有关此功能的详细信息，请参阅 [特殊池](special-pool.md)。

在 Windows Vista 和更高版本的 Windows 中，你可以将特殊池功能配置为系统范围的注册表设置或不需要重新启动的内核标志设置。 在早期版本的 Windows 中，特殊池仅作为注册表设置提供。

在 Windows Vista 和更高版本的 Windows 中，还可以使用命令行来请求按池标记的特殊池。 有关信息，请参阅 [**GFlags 命令**](gflags-commands.md)。

本部分包括以下主题。

[按池标记请求特殊池](requesting-special-pool-by-pool-tag.md)

[按分配大小请求特殊池](requesting-special-pool-by-allocation-size.md)

[取消针对特殊池的请求](canceling-requests-for-special-pool.md)

[检测超量运行和欠量运行](detecting-overruns-and-underruns.md)

**注意**   使用 *Driver Verifier* 来请求特定驱动程序分配的特殊池。 有关详细信息，请参阅 Windows 驱动程序工具包 (WDK) 的 "驱动程序验证程序" 部分中的 "特殊池" 主题。

 

 

 





