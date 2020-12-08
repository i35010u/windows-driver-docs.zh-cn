---
title: Bug 检查 0x13C INVALID_IO_BOOST_STATE
description: INVALID_IO_BOOST_STATE bug 检查的值为0x0000013C。 这表示线程退出时的 i/o 提升状态无效。 当线程退出时，此值应为零。
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
ms.openlocfilehash: a0c28d349ba08fb0b33fffa363ac27d00dd0f49f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824313"
---
# <a name="bug-check-0x13c-invalid_io_boost_state"></a>Bug 检查0x13C： \_ IO \_ 提升 \_ 状态无效


无效的 \_ IO \_ 提升 \_ 状态 bug 检查的值为0x0000013C。 这表示线程退出时的 i/o 提升状态无效。 当线程退出时，此值应为零。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="invalid_io_boost_state-parameters"></a>\_IO \_ 提升 \_ 状态参数无效


| 参数 | 描述                                             |
|-----------|---------------------------------------------------------|
| 1         | 指向具有无效提升状态的线程的指针 |
| 2         | 当前提升状态或限制计数                   |
| 3         | 预留                                                |
| 4         | 预留                                                |

 

 

 




