---
title: Bug 检查 1CC EXRESOURCE_TIMEOUT_LIVEDUMP
description: EXRESOURCE_TIMEOUT_LIVEDUMP bug 检查的值为0x000001CC。
keywords:
- Bug 检查 0x1CC EXRESOURCE_TIMEOUT_LIVEDUMP
- EXRESOURCE_TIMEOUT_LIVEDUMP
ms.date: 04/19/2018
topic_type:
- apiref
api_name:
- EXRESOURCE_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b65027cbaa9c47cc30079bb66d6e2fff4eb999da
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851284"
---
# <a name="bug-check-0x1cc-exresource_timeout_livedump"></a>Bug 检查0x1CC： EXRESOURCE \_ 超时 \_ LIVEDUMP

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


EXRESOURCE_TIMEOUT_LIVEDUMP bug 检查的值为0x000001CC。

内核 ERESOURCE 已超时。这可能表示死锁条件或严重争用，这可能会导致性能问题。


## <a name="exresource_timeout_livedump-parameters"></a>EXRESOURCE \_ TIMEOUT \_ LIVEDUMP 参数

以下参数显示在蓝色屏幕上。

参数 | 说明 
|---------|--------------|
1 | 已超时的 ERESOURCE。
2 | 检测到超时的线程
3 | ERESOURCE 争用计数
4 | 配置的超时（秒）


## <a name="see-also"></a>另请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

