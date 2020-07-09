---
title: KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOMODE （submode）
description: KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOMODE 属性允许配置 submode。
ms.assetid: B5BE7B11-66FD-476C-8141-C2210B21133C
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
ms.openlocfilehash: b8a6d32664d43cd069c47ec0fe0350e6f6bf0cbd
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128888"
---
# <a name="ksproperty_cameracontrol_extended_photomode-submode"></a>KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOMODE （submode）

KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOMODE 属性允许配置 submode。

## <a name="usage-summary"></a>使用情况摘要

以下 submodes 的定义如下。

```cpp
#define KSCAMERA_EXTENDEDPROP_PHOTOMODE_SEQUENCE_SUB_NONE       0x00000000
#define KSCAMERA_EXTENDEDPROP_PHOTOMODE_SEQUENCE_SUB_VARIABLE   0x00000001
```

\_ \_ \_ \_ \_ 常规照片序列将使用 KSCAMERA EXTENDEDPROP PHOTOMODE 序列 SUB NONE。

KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE \_ sequence \_ 子 \_ 变量用于指示照片序列是可变的。 如果指定了每帧设置，则 \_ \_ \_ \_ \_ 将在 KSCAMERA EXTENDEDPROP PHOTOMODE 结构的 submode 字段中指定 KSCAMERA EXTENDEDPROP PHOTOMODE SEQUENCE 子变量标志 \_ ， \_ 以指示可变照片序列，即使未指定任何项目设置（对于所有帧，项计数为0）。 当帧计数为1并且项计数为0时，可变照片序列会使用全局设置减少为一个帧可变照片序列。

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

**标头：** Ksmedia （包括 Ksmedia）
