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
ms.openlocfilehash: 3979c2d637f6f979d937ff486030c043e744485e
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743494"
---
# <a name="bug-check-0x1a5-usbdripsblockersurpriseremovallivedump"></a>Bug 检查 0x1A5:USB\_DRIPS\_BLOCKER\_SURPRISE\_REMOVAL\_LIVEDUMP

USB\_DRIPS\_BLOCKER\_惊讶\_删除\_LIVEDUMP bug 检查的值为 0x000001A5。 它指示 USB 设备会删除，因为它阻止 DRIPS 惊讶。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

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

