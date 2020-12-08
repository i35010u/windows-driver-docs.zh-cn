---
title: Bug 检查 0xDE POOL_CORRUPTION_IN_FILE_AREA
description: POOL_CORRUPTION_IN_FILE_AREA bug 检查的值为0x000000DE。 这表明驱动程序具有已损坏的池内存，用于存放目标为磁盘的页面。
keywords:
- Bug 检查 0xDE POOL_CORRUPTION_IN_FILE_AREA
- POOL_CORRUPTION_IN_FILE_AREA
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- POOL_CORRUPTION_IN_FILE_AREA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 26a98536c3dbdf48155c552fb185aa437d907749
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833205"
---
# <a name="bug-check-0xde-pool_corruption_in_file_area"></a>Bug 检查0xDE： \_ \_ \_ 文件区域中的池损坏 \_


\_ \_ 文件区域 bug 检查中的池损坏的 \_ \_ 值为0x000000DE。 这表明驱动程序具有已损坏的池内存，用于存放目标为磁盘的页面。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="pool_corruption_in_file_area-parameters"></a>\_ \_ \_ 文件 \_ 区域参数中的池损坏


无

<a name="cause"></a>原因
-----

当内存管理器取消对该文件的引用时，它会在池内存中发现此损坏。

 

 




