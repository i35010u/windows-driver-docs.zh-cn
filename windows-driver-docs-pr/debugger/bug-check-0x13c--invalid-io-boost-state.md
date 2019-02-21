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
ms.openlocfilehash: b3cc2bc74ddb90d7e3e62324e26668c151daafd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526433"
---
# <a name="bug-check-0x13c-invalidiobooststate"></a>Bug 检查 0x13C:无效\_IO\_BOOST\_状态


无效\_IO\_BOOST\_状态 bug 检查的值为 0x0000013C。 这表示在线程退出，I/O boost 状态无效。 线程退出时，这应为零。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="invalidiobooststate-parameters"></a>无效\_IO\_BOOST\_状态参数


| 参数 | 描述                                             |
|-----------|---------------------------------------------------------|
| 1         | 指向包含无效的提升状态的线程 |
| 2         | 当前的提升状态或中止计数                   |
| 3         | 保留                                                |
| 4         | 保留                                                |

 

 

 




