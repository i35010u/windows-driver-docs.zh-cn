---
title: Bug 检查 0x1B0 VIDEO_MINIPORT_FAILED_LIVEDUMP
description: VIDEO_MINIPORT_FAILED_LIVEDUMP bug 检查具有 0x000001B0 值。 它指示 DXGKRNL 检测到的微型端口驱动程序问题和已捕获的实时转储收集调试信息。
keywords:
- Bug 检查 0x1B0 VIDEO_MINIPORT_FAILED_LIVEDUMP
- VIDEO_MINIPORT_FAILED_LIVEDUMP
ms.date: 01/08/2018
topic_type:
- apiref
api_name:
- VIDEO_MINIPORT_FAILED_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4c1c4e47caa8d9bf393f914a15c04e707e66e189
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239048"
---
# <a name="bug-check-0x1b0-videominiportfailedlivedump"></a>Bug 检查 0x1B0：视频\_微型端口\_失败\_LIVEDUMP

视频\_微型端口\_失败\_LIVEDUMP bug 检查的值为 0x000001B0。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="videominiportfailedlivedump-parameters"></a>视频\_微型端口\_失败\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1| 原因代码。 值：0x1:*添加设备失败。* 0x2:*启动失败的设备。*|
|2| NTSTATUS|
|3| 保留。 |
|4| 保留。 |


## <a name="cause"></a>原因
-----
DXGKRNL 检测到问题和已捕获的实时转储收集调试信息。 这些 livedumps 由 dxgkrnl 微型端口驱动程序失败时触发。

（此代码可以永远不会用于实际的执行错误检查; 它用于标识实时转储）。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

 


 




