---
title: 配置特殊的池
description: 配置特殊的池
ms.assetid: a6c90e88-8d67-47e8-8862-b7585a5d8bec
keywords:
- GFlags、 内核特殊池配置
- 内核特殊池
- 特殊的池
- 池标记和特殊的池
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13439d575fa762306539fe547793a6bba0b55305
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521469"
---
# <a name="configuring-special-pool"></a>配置特殊的池


## <span id="ddk_configuring_kernel_special_pool_dtools"></span><span id="DDK_CONFIGURING_KERNEL_SPECIAL_POOL_DTOOLS"></span>


Gflags*特殊池*功能指示 Windows 请求内存分配保留的内存池中时内存分配了指定的池标记或指定的大小范围内。

有关此功能的详细信息，请参阅[特殊池](special-pool.md)。

在 Windows Vista 和更高版本的 Windows 中，可以将特殊池功能配置为整个系统的注册表设置或为一个内核标志设置，不需要重新启动。 在早期版本的 Windows 中，特殊的池是仅作为注册表设置。

在 Windows Vista 和更高版本的 Windows 中，还可以使用命令行来请求特殊标记，池的池。 有关信息，请参阅[ **GFlags 命令**](gflags-commands.md)。

本部分包括以下主题。

[请求特殊标记，池的池](requesting-special-pool-by-pool-tag.md)

[请求特殊池分配大小](requesting-special-pool-by-allocation-size.md)

[为特殊池取消请求](canceling-requests-for-special-pool.md)

[检测溢出和不足](detecting-overruns-and-underruns.md)

**请注意**  使用*Driver Verifier*请求特殊池分配的特定驱动程序。 有关详细信息，请参阅"驱动程序验证程序"部分的 Windows Driver Kit (WDK) 中的"特殊池"主题。

 

 

 





