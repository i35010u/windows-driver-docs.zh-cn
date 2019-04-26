---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE
description: KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE 属性允许子模式进行配置。
ms.assetid: B5BE7B11-66FD-476C-8141-C2210B21133C
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: dc6d1c9c9a16088fb7579f9e7fd8c7ba85d2af60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324804"
---
# <a name="kspropertycameracontrolextendedphotomode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE

KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE 属性允许子模式进行配置。

## <a name="usage-summary"></a>使用情况摘要

以下 submodes 定义，如下所示。

```cpp
#define KSCAMERA_EXTENDEDPROP_PHOTOMODE_SEQUENCE_SUB_NONE       0x00000000
#define KSCAMERA_EXTENDEDPROP_PHOTOMODE_SEQUENCE_SUB_VARIABLE   0x00000001
```

KSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_序列\_SUB\_无由正则照片序列。

KSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_序列\_SUB\_变量用于指示照片序列是变量。 如果指定每个帧设置，KSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_序列\_SUB\_将 KSCAMERA 的子模式字段中指定变量标志\_EXTENDEDPROP\_PHOTOMODE 结构来指示变量照片序列，即使没有项目设置中指定 （项计数为 0 表示所有帧）。 当帧计数为 1 和项的计数为 0 时，变量照片序列可以减少到一帧变量照片序列使用全局设置。

下面是一个定义 KSCAMERA\_EXTENDEDPROP\_PHOTOMODE ksmedia.h 中定义的结构

```cpp
typedef struct tagKSCAMERA_EXTENDEDPROP_PHOTOMODE {  
    ULONG       RequestedHistoryFrames;  
    ULONG       MaxHistoryFrames;  
    ULONG       SubMode;  
    ULONG       Reserved;  
} KSCAMERA_EXTENDEDPROP_PHOTOMODE, *PKSCAMERA_EXTENDEDPROP_PHOTOMODE;
```

变量照片序列模式上的照片序列具有以下独特的特征。

-   始终使用有限的照片序列。

-   每帧的帧计数大于 0 时，会应用设置。

-   该驱动程序将自动停止照片序列末尾而无需 KS\_VideoControlFlag\_指定 StopPhotoSequenceCapture 触发器时循环计数大于 0。

-   最后一个示例必须标有 KSSTREAM\_标头\_OPTIONSF\_ENDOFPHOTOSEQUENCE 标志。

-   捕获管道从驱动程序将不删除任何示例。

-   管道和驱动程序都不\\MFT0 生成任何照片的缩略图。

此属性是异步的不取消。

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
