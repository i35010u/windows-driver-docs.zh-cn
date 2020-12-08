---
title: 'KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOMODE (submode) '
description: KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOMODE 属性允许配置 submode。
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0e4bbfcda44af8f530f73471d9229e8befa3c61b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837859"
---
# <a name="ksproperty_cameracontrol_extended_photomode-submode"></a>KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOMODE (submode) 

KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOMODE 属性允许配置 submode。

## <a name="usage-summary"></a>使用情况摘要

以下 submodes 的定义如下。

```cpp
#define KSCAMERA_EXTENDEDPROP_PHOTOMODE_SEQUENCE_SUB_NONE       0x00000000
#define KSCAMERA_EXTENDEDPROP_PHOTOMODE_SEQUENCE_SUB_VARIABLE   0x00000001
```

\_ \_ \_ \_ \_ 常规照片序列将使用 KSCAMERA EXTENDEDPROP PHOTOMODE 序列 SUB NONE。

KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE \_ sequence \_ 子 \_ 变量用于指示照片序列是可变的。 如果指定了每帧设置，则 \_ \_ \_ \_ \_ 将在 KSCAMERA EXTENDEDPROP PHOTOMODE 结构的 submode 字段中指定 KSCAMERA EXTENDEDPROP PHOTOMODE SEQUENCE 子变量标志 \_ ， \_ 以指示可变的照片序列，即使未指定任何项设置 (项计数对于) 的所有帧都为0。 当帧计数为1并且项计数为0时，可变照片序列会使用全局设置减少为一个帧可变照片序列。

下面是 KSCAMERA \_ \_ 中定义的 EXTENDEDPROP PHOTOMODE 结构的定义：

```cpp
typedef struct tagKSCAMERA_EXTENDEDPROP_PHOTOMODE {  
    ULONG       RequestedHistoryFrames;  
    ULONG       MaxHistoryFrames;  
    ULONG       SubMode;  
    ULONG       Reserved;  
} KSCAMERA_EXTENDEDPROP_PHOTOMODE, *PKSCAMERA_EXTENDEDPROP_PHOTOMODE;
```

可变照片序列模式对于照片序列具有以下独特特征。

- 始终使用有限照片序列。

- 帧计数大于0时应用每帧设置。

- \_ \_ 如果指定的循环计数大于0，则驱动程序将在结束时自动停止照片序列，而无需使用 KS VideoControlFlag StopPhotoSequenceCapture 触发器。

- 最后一个示例必须标记有 KSSTREAM \_ 标头 \_ OPTIONSF \_ ENDOFPHOTOSEQUENCE 标志。

- 捕获管道不会从驱动程序中删除任何示例。

- 管道和驱动程序都不会 \\ 生成任何照片缩略图。 MFT0

此属性是异步的，不可取消。

## <a name="requirements"></a>要求

**标头：** Ksmedia (包含 Ksmedia) 
