---
title: 选择性 Opt-Out POOL_NX_OPTOUT
description: 你可以全局启用一组驱动程序源文件的 "不执行 (NX) 池" 选择机制，然后使用 POOL_NX_OPTOUT 为一个或多个选定的源文件重写此选择机制。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a6097df8a7dec346eec0f694dea226a7ca834555
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822299"
---
# <a name="selective-opt-out-pool_nx_optout"></a>选择性选择退出： POOL \_ NX \_ 选择


你可以全局启用一组驱动程序源文件的 "不执行 (" NX) 池选择机制，然后使用 POOL NX 选择为一个或多个所选源文件重写此选择机制 \_ \_ 。 这允许选定的源文件继续使用可执行的非分页内存。 可以将 POOL \_ nx \_ 选择选择 out 机制与 pool \_ NX \_ OPTIN 或 pool \_ nx \_ OPTIN \_ 自动选择机制一起使用。 有关详细信息，请参阅 [NX 池 Opt-In 机制](nx-pool-opt-in-mechanisms.md)。

若要使用 POOL \_ NX \_ 输出选择退出机制替代选定源文件中的选择机制，请将以下定义添加到此文件中：

`#define POOL_NX_OPTOUT 1`

此定义将覆盖所选文件中的全局选择加入设置，并阻止替换 **非分页池** 常量名称的实例。 在文件中 **非分页池** 的第一个实例之前，将此定义插入到文件中。

\_ \_ 在源文件中使用 POOL NX 选择选择 out 机制的替代方法是：使用 NonPagedPoolExecute 将文件中的每个 **非分页池** 实例显式替换为 **NonPagedPoolExecute**。

 

 




