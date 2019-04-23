---
title: Bug 检查 0x11F INVALID_DRIVER_HANDLE
description: INVALID_DRIVER_HANDLE bug 检查具有 0x0000011F 值。 这表示有人关闭了之间插入驱动程序对象和引用了句柄的驱动程序的初始句柄。
ms.assetid: A669256B-737D-4215-8E0E-5500D7704F4E
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
ms.openlocfilehash: b6afd88545c1043e19c725337742b4b10f5dc5c7
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902931"
---
# <a name="bug-check-0x11f-invaliddriverhandle"></a>Bug 检查 0x11F：无效\_驱动程序\_处理


无效\_驱动程序\_句柄 bug 检查的值为 0x0000011F。 这表示有人关闭了之间插入驱动程序对象和引用了句柄的驱动程序的初始句柄。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="invaliddriverhandle-parameters"></a>无效\_驱动程序\_句柄参数


| 参数 | 描述                                         |
|-----------|-----------------------------------------------------|
| 1         | 驱动程序对象的句柄值。             |
| 2         | 尝试引用该对象返回的状态。 |
| 3         | PDRIVER 地址\_对象。                 |
| 4         | 保留                                            |

 

 

 




