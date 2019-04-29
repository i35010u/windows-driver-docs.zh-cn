---
title: Bug Check 0x141 VIDEO_ENGINE_TIMEOUT_DETECTED
description: VIDEO_ENGINE_TIMEOUT_DETECTED bug 检查具有 0x00000141 值。 这表示引擎未能及时响应的显示其中一个。
ms.assetid: 0912495D-DE6D-4064-BD66-DA6145889821
keywords:
- Bug Check 0x141 VIDEO_ENGINE_TIMEOUT_DETECTED
- VIDEO_ENGINE_TIMEOUT_DETECTED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_ENGINE_TIMEOUT_DETECTED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b9696710c1c4274e89895ddc7a8b08023e3c9b32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360106"
---
# <a name="bug-check-0x141-videoenginetimeoutdetected"></a>Bug 检查 0x141：视频\_引擎\_超时\_检测到


视频\_引擎\_超时\_检测到错误检查的值为 0x00000141。 这表示引擎未能及时响应的显示其中一个。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="videoenginetimeoutdetected-parameters"></a>视频\_引擎\_超时\_检测到参数


| 参数 | 描述                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | 指向内部 TDR 恢复上下文的可选 (TDR\_恢复\_上下文)。 |
| 2         | 负责的设备驱动程序模块 （例如所有者标记） 到指针。          |
| 3         | 辅助驱动程序特定存储桶键。                                |
| 4         | 可选的内部上下文相关的数据。                                   |

 

<a name="remarks"></a>备注
-------

辅助标记 {270A33FD-3DA6-460D-BA89-3C1BAE21E39B} 的数据包含其他 TDR 相关数据。 使用.enumtag 若要查看的数据。

 

 




