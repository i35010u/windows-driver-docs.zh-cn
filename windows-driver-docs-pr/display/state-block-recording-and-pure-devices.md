---
title: 状态块记录和单纯设备
description: 状态块记录和单纯设备
keywords:
- DirectX 8.0 发行说明了 WDK Windows 2000 显示、纯设备、状态块处理
- 纯设备 WDK DirectX 8.0，状态块处理
- 状态块处理 WDK DirectX 8。0
- 状态块处理 WDK DirectX 8.0，纯设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eac14a47a19168f859f69dd3d4034d0c3d69683e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820801"
---
# <a name="state-block-recording-and-pure-devices"></a>状态块记录和单纯设备


## <span id="ddk_state_block_recording_and_pure_devices_gg"></span><span id="DDK_STATE_BLOCK_RECORDING_AND_PURE_DEVICES_GG"></span>


在纯设备模式下运行的设备的状态块处理方式不同。 在此模式下，会将状态块控制 DP2 标记 (D3DDP2OP \_ STATESET) 发送到 **dwOperations** 字段) 中 (新操作类型的驱动程序。 此新操作类型为 D3DHAL \_ STATESETCREATE。

 

 





