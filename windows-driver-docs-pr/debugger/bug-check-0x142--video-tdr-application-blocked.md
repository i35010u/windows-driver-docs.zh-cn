---
title: Bug 检查 0x142 VIDEO_TDR_APPLICATION_BLOCKED
description: VIDEO_TDR_APPLICATION_BLOCKED bug 检查具有 0x00000142 值。 这表示应用程序已被阻止访问图形硬件。
ms.assetid: B97FCA51-C368-4144-A364-50135A8DE836
keywords:
- Bug 检查 0x142 VIDEO_TDR_APPLICATION_BLOCKED
- VIDEO_TDR_APPLICATION_BLOCKED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_TDR_APPLICATION_BLOCKED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4fd4707a1d3d175059f8098c8e2ce5c35ceb2a77
ms.sourcegitcommit: 1a5d7884cec9dd8d2b85242bee78b56a1cf8e4c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2019
ms.locfileid: "58761846"
---
# <a name="bug-check-0x142-videotdrapplicationblocked"></a>Bug 检查 0x142：视频\_TDR\_应用程序\_已阻止


视频\_TDR\_应用程序\_已阻止错误检查的值为 0x00000142。 这表示应用程序已被阻止访问图形硬件。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="videotdrapplicationblocked-parameters"></a>视频\_TDR\_应用程序\_已阻止参数


| 参数 | 描述                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | 指向内部 TDR 恢复上下文的可选 (TDR\_恢复\_上下文)。 |
| 2         | 负责的设备驱动程序模块 （例如所有者标记） 到指针。          |
| 3         | 辅助驱动程序特定存储桶键。                                |
| 4         | 正在阻止访问 GPU 的进程 id。                     |

 

<a name="remarks"></a>备注
-------

[ **！ 分析**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息和确定根本原因非常有帮助。
辅助标记 {270A33FD-3DA6-460D-BA89-3C1BAE21E39B} 的数据包含其他 TDR 相关数据。 使用[ **.enumtag （枚举辅助回调数据）** ](-enumtag--enumerate-secondary-callback-data-.md)若要查看的数据。

 

 




