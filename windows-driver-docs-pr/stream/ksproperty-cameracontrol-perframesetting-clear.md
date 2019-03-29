---
title: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_清除
description: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_KSPROPERTY 中定义的清除的属性 ID\_CAMERACONTROL\_PERFRAMESETTING\_属性可用于清除每个帧中驱动程序的设置。
ms.assetid: CCFB4226-36A7-4A5A-8A65-F8E9F281AAA4
keywords:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_CLEAR 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_CLEAR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5cf0889ed1e914bfbafb63aef2a4f2077ba6d58b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577095"
---
# <a name="kspropertycameracontrolperframesettingclear"></a>KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_清除

**KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_清除**中定义的属性 ID **KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_属性**用于清除驱动程序中的每个帧设置。 这是设置仅控制并且没有任何负载。 这通常用于完成时 （取消准备） 照片序列。

## <a name="photo-sequence-usage-summary"></a>照片序列使用情况摘要


**无限照片序列**

准备照片 sequence 命令发出应用客户端时，照片序列将进入准备状态。 驱动程序 pin，则可能创建或已创建具体取决于热启动状态，并且无论它是第一次准备照片序列。 完成准备状态后，则将为正在运行状态，并为就绪状态照片序列传输过驱动程序 pin。 然后，驱动程序将开始填充其内部历史记录缓冲区。

照片序列启动后触发 KS\_VideoControlFlag\_收到 StartPhotoSequenceCapture、 照片序列将传输到捕获状态和驱动程序 pin 将保持运行状态。 在进入此状态，该驱动程序将开始填充将来帧和交付以及任何将来的帧的所有可用的历史记录框架。

照片序列停止后触发 KS\_VideoControlFlag\_收到 StopPhotoSequenceCapture、 为就绪状态照片序列上流动传到和驱动程序 pin 将保持运行状态。 在进入此状态下，驱动程序将停止将帧送回管道并开始改为填充其内部历史记录缓冲区。

照片序列进入之状态时应用客户端发出的完成命令。 驱动程序 pin 将进行过的从运行状态为已暂停或已停止状态由具体取决于是否启用热状态的管道。

**有限的照片序列**

准备照片 sequence 命令发出应用客户端时，照片序列将进入准备状态。 驱动程序 pin，则可能创建或已创建具体取决于热启动状态，并且无论它是第一次准备照片序列。 完成准备状态后，则将为正在运行状态，并为就绪状态照片序列传输过驱动程序 pin。 然后，驱动程序将开始填充其内部历史记录缓冲区。

照片序列启动后触发 KS\_VideoControlFlag\_收到 StartPhotoSequenceCapture、 照片序列将传输到捕获状态和驱动程序 pin 将保持运行状态。 在进入此状态，该驱动程序将开始填充将来帧和交付以及任何将来的帧的所有可用的历史记录框架。

后指定照片中的最后一帧序列已被标记为 KSSTREAM\_标头\_OPTIONSF\_ENDOFPHOTOSEQUENCE 和传递，照片序列上流动传到到等待状态，驱动程序 pin 仍保留在运行状态。 在进入此状态，该驱动程序应停止将任何帧送回管道。 该驱动程序可以选择不会生成任何帧或启动填充其内部历史记录缓冲区。 确切行为由 OEM 决定。

照片序列停止后触发 KS\_VideoControlFlag\_收到 StopPhotoSequenceCapture、 为就绪状态照片序列上流动传到和驱动程序 pin 将保持运行状态。 在进入此状态下，驱动程序启动与传递到管道不帧填充其内部历史记录缓冲区。

照片序列进入之状态时应用客户端发出的完成命令。 驱动程序 pin 将进行过的从运行状态为已暂停或已停止状态由具体取决于是否启用热状态的管道。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
