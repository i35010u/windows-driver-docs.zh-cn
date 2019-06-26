---
title: Bug 检查 0xDE POOL_CORRUPTION_IN_FILE_AREA
description: POOL_CORRUPTION_IN_FILE_AREA bug 检查具有 0x000000DE 值。 这表示一个驱动程序损坏了用来存放目标为磁盘的页池内存。
ms.assetid: 6394e0fa-76ee-4924-8aa3-d10a4d57c6e8
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
ms.openlocfilehash: d1c19c52d5a10640af0b884bffbb0427700b025d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361577"
---
# <a name="bug-check-0xde-poolcorruptioninfilearea"></a>Bug 检查 0xDE：池\_损坏\_IN\_文件\_区域


在池中\_损坏\_IN\_文件\_区域 bug 检查的值为 0x000000DE。 这表示一个驱动程序损坏了用来存放目标为磁盘的页池内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="poolcorruptioninfilearea-parameters"></a>池\_损坏\_IN\_文件\_区域参数


无

<a name="cause"></a>原因
-----

当内存管理器取消引用该文件时，它发现这种损坏池内存中。

 

 




