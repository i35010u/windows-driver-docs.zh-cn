---
title: KSPROPERTY \_ CAMERACONTROL \_ PERFRAMESETTING \_ CLEAR
description: '\_ \_ \_ KSPROPERTY CAMERACONTROL PERFRAMESETTING 属性中定义的 KSPROPERTY CAMERACONTROL PERFRAMESETTING clear 属性 \_ ID \_ \_ 用于清除驱动程序中的每帧设置。'
keywords:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_CLEAR 流媒体设备
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
ms.openlocfilehash: 6ea1eb2d7a5d86b7f8c9fb4c7b9605ecb18513f0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832059"
---
# <a name="ksproperty_cameracontrol_perframesetting_clear"></a>KSPROPERTY \_ CAMERACONTROL \_ PERFRAMESETTING \_ CLEAR

**KSPROPERTY \_ CAMERACONTROL \_ PERFRAMESETTING \_ 属性** 中定义的 **KSPROPERTY \_ CAMERACONTROL \_ PERFRAMESETTING \_ clear** 属性 ID 用于清除驱动程序中的每帧设置。 这是一个仅设置控件，此控件没有有效负载。 这通常在完成 (unpreparing) 照片序列时使用。

## <a name="photo-sequence-usage-summary"></a>照片序列使用情况摘要


**无限照片序列**

当应用客户端发出准备照片序列命令时，照片序列将进入准备状态。 可能会创建或已创建驱动程序 pin，具体取决于热启动状态以及是否是第一次准备照片序列。 准备状态完成后，驱动程序的 pin 码将被过渡为 "正在运行" 状态，照片序列上流动为 "就绪" 状态。 然后，该驱动程序将开始填充其内部历史记录缓冲区。

收到照片序列启动触发器 KS \_ VideoControlFlag \_ StartPhotoSequenceCapture 后，照片序列会传输到捕获状态，驱动程序 pin 仍处于 "正在运行" 状态。 进入此状态之后，驱动程序将开始填写未来的帧，并提供所有可用的历史记录帧以及任何将来的帧。

收到照片序列停止触发器 KS \_ VideoControlFlag \_ StopPhotoSequenceCapture 后，照片序列上流动为就绪状态，驱动程序 pin 仍处于运行状态。 进入此状态之后，驱动程序将停止将帧传递回管道并改为开始填充其内部历史记录缓冲区。

当应用客户端发出完成命令时，照片序列将进入 unprepare 状态。 驱动程序 pin 将从正在运行状态过渡到暂停或停止状态，具体取决于是否启用了热状态。

**有限照片序列**

当应用客户端发出准备照片序列命令时，照片序列将进入准备状态。 可能会创建或已创建驱动程序 pin，具体取决于热启动状态以及是否是第一次准备照片序列。 准备状态完成后，驱动程序的 pin 码将被过渡为 "正在运行" 状态，照片序列上流动为 "就绪" 状态。 然后，该驱动程序将开始填充其内部历史记录缓冲区。

收到照片序列启动触发器 KS \_ VideoControlFlag \_ StartPhotoSequenceCapture 后，照片序列会传输到捕获状态，驱动程序 pin 仍处于 "正在运行" 状态。 进入此状态之后，驱动程序将开始填写未来的帧，并提供所有可用的历史记录帧以及任何将来的帧。

在照片序列中指定的最后一个帧已标记为 KSSTREAM \_ 标头 \_ OPTIONSF \_ ENDOFPHOTOSEQUENCE 并传送后，照片序列上流动到等待状态，驱动程序 pin 仍处于 "正在运行" 状态。 进入此状态之后，驱动程序应停止将任何帧传递回管道。 驱动程序可以选择不生成任何帧或开始填充其内部历史记录缓冲区。 确切的行为取决于 OEM。

收到照片序列停止触发器 KS \_ VideoControlFlag \_ StopPhotoSequenceCapture 后，照片序列上流动为就绪状态，驱动程序 pin 仍处于运行状态。 进入此状态后，驱动程序将开始填充其内部历史记录缓冲区，而不会将帧传递到管道。

当应用客户端发出完成命令时，照片序列将进入 unprepare 状态。 驱动程序 pin 将从正在运行状态过渡为已暂停或已停止状态，具体取决于是否启用了热状态。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
