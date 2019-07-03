---
title: Bug 检查 0x1A5 USB_DRIPS_BLOCKER_SURPRISE_REMOVAL_LIVEDUMP
description: USB_DRIPS_BLOCKER_SURPRISE_REMOVAL_LIVEDUMP bug 检查具有 0x000001A5 值。 它指示 USB 设备会删除，因为它阻止 DRIPS 惊讶。
keywords:
- Bug 检查 0x1A5 USB_DRIPS_BLOCKER_SURPRISE_REMOVAL_LIVEDUMP
- USB_DRIPS_BLOCKER_SURPRISE_REMOVAL_LIVEDUMP
ms.date: 01/10/2019
topic_type:
- apiref
api_name:
- USB_DRIPS_BLOCKER_SURPRISE_REMOVAL_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 11748f2d0fffef755d1d4eea2758f423a0fa4688
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519752"
---
# <a name="bug-check-0x1a5-usbdripsblockersurpriseremovallivedump"></a>Bug 检查 0x1A5：USB\_DRIPS\_BLOCKER\_SURPRISE\_REMOVAL\_LIVEDUMP

USB\_DRIPS\_BLOCKER\_惊讶\_删除\_LIVEDUMP bug 检查的值为 0x000001A5。 它指示 USB 设备会删除，因为它阻止 DRIPS 惊讶。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="usbdripsblockersurpriseremovallivedump-parameters"></a>USB\_DRIPS\_BLOCKER\_惊讶\_删除\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1| 阻止设备的 PDO。|
|2| 保留。 |
|3| 保留。 |
|4| 保留。 |

## <a name="cause"></a>原因
-----

USB 设备正在阻止从关闭在现代待机状态的最高级别控制器并将结果是删除惊讶。

（此代码可以永远不会用于实际的执行错误检查; 它用于标识实时转储）。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

