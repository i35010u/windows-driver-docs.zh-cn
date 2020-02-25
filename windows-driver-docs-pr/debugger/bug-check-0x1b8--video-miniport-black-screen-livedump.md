---
title: Bug 检查 0x1B8 VIDEO_MINIPORT_BLACK_SCREEN_LIVEDUMP
description: VIDEO_MINIPORT_BLACK_SCREEN_LIVEDUMP bug 检查的值为0x000001B8。 它指示用户为黑色屏幕方案启动了微型端口实时转储。
keywords:
- Bug 检查 0x1B8 VIDEO_MINIPORT_BLACK_SCREEN_LIVEDUMP
- VIDEO_MINIPORT_BLACK_SCREEN_LIVEDUMP
ms.date: 02/20/2020
topic_type:
- apiref
api_name:
- VIDEO_MINIPORT_BLACK_SCREEN_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: db47e16744f50163f04b7bb1e74c85149271a146
ms.sourcegitcommit: e018ef208a38bc871b25d9fb72c2501fe4a5f965
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77477150"
---
# <a name="bug-check-0x1b8-video_miniport_black_screen_livedump"></a>Bug 检查0x1B8：视频\_微型端口\_黑色\_屏幕\_LIVEDUMP

视频\_微型端口\_黑色\_屏幕\_LIVEDUMP bug 检查的值为0x000001B8。 它指示用户为黑色屏幕方案启动了微型端口实时转储。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="video_miniport_black_screen_livedump-parameters"></a>视频\_微型端口\_黑色\_屏幕\_LIVEDUMP 参数

|参数|说明|
|--- |--- |
|1| 触发微型端口黑色实时转储的源-下面列出。|
|2| 保留。 |
|3| 保留。 |
|4| 保留。 |

**源值**

0x1：黑色屏幕热键生成微型端口黑色屏幕直播转储

0x2：卷组合键生成微型端口黑色屏幕直播转储

0x4：内部生成的微型端口黑色屏幕直播转储

0x8：长电源按钮保留（LPBH）生成的微型端口黑色屏幕直播转储

## <a name="cause"></a>原因

用户为黑色屏幕方案启动了微型端口实时转储。 查看触发的实时转储的源的参数1的值。

（此代码永远不能用于实际错误检查; 它用于标识实时转储。）

## <a name="see-also"></a>另请参阅

[Bug 检查代码引用](bug-check-code-reference2.md)
