---
title: Bug 检查 0x13C INVALID_IO_BOOST_STATE
description: INVALID_IO_BOOST_STATE bug 检查具有 0x0000013C 值。 这表示在线程退出，I/O boost 状态无效。 线程退出时，这应为零。
ms.assetid: BDCD8A3A-1F26-41A4-95B0-9B2CEBD333AC
keywords:
- Bug 检查 0x13C INVALID_IO_BOOST_STATE
- INVALID_IO_BOOST_STATE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_IO_BOOST_STATE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b7e37f5ec6b3ec9c4c7bcd06ab21983adb18da1f
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520206"
---
# <a name="bug-check-0x13c-invalidiobooststate"></a>Bug 检查 0x13C：无效\_IO\_BOOST\_状态


无效\_IO\_BOOST\_状态 bug 检查的值为 0x0000013C。 这表示在线程退出，I/O boost 状态无效。 线程退出时，这应为零。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="invalidiobooststate-parameters"></a>无效\_IO\_BOOST\_状态参数


| 参数 | 描述                                             |
|-----------|---------------------------------------------------------|
| 1         | 指向包含无效的提升状态的线程 |
| 2         | 当前的提升状态或中止计数                   |
| 3         | 保留                                                |
| 4         | 保留                                                |

 

 

 




