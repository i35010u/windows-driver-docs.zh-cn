---
title: 状态块记录和单纯设备
description: 状态块记录和单纯设备
ms.assetid: 9959d361-aa92-4209-8f81-deba96498941
keywords:
- DirectX 8.0 版本显示注释 WDK Windows 2000 中，纯设备状态阻止处理
- 纯设备 WDK DirectX 8.0 状态块处理
- 状态块处理 WDK DirectX 8.0
- 处理 WDK DirectX 8.0，纯设备状态块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44c40c708ebf6429de76853bc5112dcbbb574b13
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376013"
---
# <a name="state-block-recording-and-pure-devices"></a>状态块记录和单纯设备


## <span id="ddk_state_block_recording_and_pure_devices_gg"></span><span id="DDK_STATE_BLOCK_RECORDING_AND_PURE_DEVICES_GG"></span>


状态块处理是不同的设备在纯设备模式下运行。 在此模式下，状态块 control DP2 令牌 (D3DDP2OP\_状态集) 发送到具有新的操作类型的驱动程序 (在**dwOperations**字段)。 此新的操作类型是 D3DHAL\_STATESETCREATE。

 

 





