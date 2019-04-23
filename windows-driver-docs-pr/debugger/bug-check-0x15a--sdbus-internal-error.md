---
title: Bug Check 0x15A SDBUS_INTERNAL_ERROR
description: SDBUS_INTERNAL_ERROR bug 检查具有 0x0000015A 值。 这表示 SD 附加设备上发生了不可恢复的硬件故障。
ms.assetid: C5FBE617-DADD-452C-A1BC-A0DE228FF2DE
keywords:
- Bug Check 0x15A SDBUS_INTERNAL_ERROR
- SDBUS_INTERNAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SDBUS_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 368734b10bc0b03f3562e82f8ee8af3a2d763f61
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903413"
---
# <a name="bug-check-0x15a-sdbusinternalerror"></a>Bug 检查 0x15A：SDBUS\_INTERNAL\_ERROR


SDBUS\_内部\_错误 bug 检查的值为 0x0000015A。 这表示 SD 附加设备上发生了不可恢复的硬件故障。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="sdbusinternalerror-parameters"></a>SDBUS\_内部\_错误参数


| 参数 | 描述                                                    |
|-----------|----------------------------------------------------------------|
| 1         | 指向内部导致失败的 SD 工作数据包 |
| 2         | 指针的控制器套接字信息                      |
| 3         | 指向 SD 请求数据包发送到总线驱动程序   |
| 4         | 保留                                                       |

 

 

 




