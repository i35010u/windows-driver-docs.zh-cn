---
title: Bug 检查 0x11F INVALID_DRIVER_HANDLE
description: INVALID_DRIVER_HANDLE bug 检查的值为0x0000011F。 这表明有人在插入驱动程序对象和引用句柄之间关闭了驱动程序的初始句柄。
keywords:
- Bug 检查 0x11F INVALID_DRIVER_HANDLE
- INVALID_DRIVER_HANDLE
ms.date: 01/30/2019
topic_type:
- apiref
api_name:
- INVALID_DRIVER_HANDLE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0e3dd4d54d0c364d75bd6bec8a832350b079fc7c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816969"
---
# <a name="bug-check-0x11f-invalid_driver_handle"></a>Bug 检查0x11F： \_ 驱动程序 \_ 句柄无效


无效 \_ 驱动程序 \_ 句柄 bug 检查的值为0x0000011F。 这表明有人在插入驱动程序对象和引用句柄之间关闭了驱动程序的初始句柄。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="invalid_driver_handle-parameters"></a>\_驱动程序 \_ 句柄参数无效


| 参数 | 描述                                         |
|-----------|-----------------------------------------------------|
| 1         | 驱动程序对象的句柄值。             |
| 2         | 尝试引用对象时返回的状态。 |
| 3         | PDRIVER 对象的地址 \_ 。                 |
| 4         | 预留                                            |

 

 

 




