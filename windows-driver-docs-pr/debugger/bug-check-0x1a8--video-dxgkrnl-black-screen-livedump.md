---
title: Bug 检查 0x1A8 VIDEO_DXGKRNL_BLACK_SCREEN_LIVEDUMP
description: VIDEO_DXGKRNL_BLACK_SCREEN_LIVEDUMP bug 检查具有 0x000001A8 值。 它指示发生了黑色屏幕使用情况的用户启动 DXGKRNL 实时转储。
keywords:
- Bug 检查 0x1A8 VIDEO_DXGKRNL_BLACK_SCREEN_LIVEDUMP
- VIDEO_DXGKRNL_BLACK_SCREEN_LIVEDUMP
ms.date: 01/28/2018
topic_type:
- apiref
api_name:
- VIDEO_DXGKRNL_BLACK_SCREEN_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 015df308d6d2f30e2efbeb4b4b50521c8e0d419f
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743518"
---
# <a name="bug-check-0x1a8-videodxgkrnlblackscreenlivedump"></a>Bug 检查 0x1A8:视频\_DXGKRNL\_黑色\_屏幕\_LIVEDUMP

视频\_DXGKRNL\_黑色\_屏幕\_LIVEDUMP bug 检查的值为 0x000001A8。 它指示发生了黑色屏幕使用情况的用户启动 DXGKRNL 实时转储。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="videodxgkrnlblackscreenlivedump-parameters"></a>视频\_DXGKRNL\_黑色\_屏幕\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1| 触发 DXGKRNL 黑屏实时转储-下面列出的源。|
|2| 保留。 |
|3| 保留。 |
|4| 保留。 |

**源值**

     0x1: Black screen hotkey generated DXGKRNL black screen live dump
     0x2: Volume combo key generated DXGKRNL black screen live dump
     0x4: Internal generated DXGKRNL black screen live dump
     0x8: Long Power Button Hold (LPBH) generated DXGKRNL black screen live dump


## <a name="cause"></a>原因
-----

用户启动的 DXGKRNL 实时转储的黑色屏幕使用情况。 请参阅的源触发的实时转储的参数 1 的值。 

（此代码可以永远不会用于实际的执行错误检查; 它用于标识实时转储）。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)







 




