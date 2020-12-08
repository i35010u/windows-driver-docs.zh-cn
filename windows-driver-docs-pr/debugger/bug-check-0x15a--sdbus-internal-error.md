---
title: Bug 检查 0x15A SDBUS_INTERNAL_ERROR
description: SDBUS_INTERNAL_ERROR bug 检查的值为0x0000015A。 这表示 SD 连接的设备上发生了不可恢复的硬件故障。
keywords:
- Bug 检查 0x15A SDBUS_INTERNAL_ERROR
- SDBUS_INTERNAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SDBUS_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 76d546829214a3350435a696a4547b16d52ead8c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803987"
---
# <a name="bug-check-0x15a-sdbus_internal_error"></a>Bug 检查0x15A： SDBUS \_ 内部 \_ 错误


SDBUS \_ 内部 \_ 错误 bug 检查的值为0x0000015A。 这表示 SD 连接的设备上发生了不可恢复的硬件故障。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="sdbus_internal_error-parameters"></a>SDBUS \_ 内部 \_ 错误参数


| 参数 | 描述                                                    |
|-----------|----------------------------------------------------------------|
| 1         | 指向导致故障的内部 SD 工作数据包的指针 |
| 2         | 指针控制器套接字信息                      |
| 3         | 指向向下发送到总线驱动程序的 SD 请求数据包的指针   |
| 4         | 预留                                                       |

 

 

 




