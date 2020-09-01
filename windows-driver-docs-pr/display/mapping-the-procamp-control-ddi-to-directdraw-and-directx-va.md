---
title: 将 DDI 的 ProcAmp 控件映射到 DirectDraw 和 DirectX VA
description: 通过 DirectDraw 的 [运动补偿回调函数](motion-compensation-callbacks.md)访问 ProcAmp 控件功能，并将其映射到 [ProcAmp 控制 DDI](./procamp-control-ddi.md)。
ms.assetid: ca2b92d9-7f3d-45b9-8841-43915dd4237d
keywords:
- ProcAmp WDK DirectX VA，映射 ProcAmp 控制 DDI
- 映射 ProcAmp 控件 DDI
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: b510db5e7d77f4843248b66a6e77c1e958a58aa2
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065147"
---
# <a name="map-the-procamp-control-ddi-to-directdraw-and-directx-va"></a>将 DDI 的 ProcAmp 控件映射到 DirectDraw 和 DirectX VA

必须通过 DirectDraw 的 [运动补偿回调函数](motion-compensation-callbacks.md) 访问 ProcAmp 控件功能， [ProcAmp 控件 DDI](./procamp-control-ddi.md) 可映射到该函数。 有关将 DirectX VA DDI 映射到 DirectDraw 的运动补偿回调的详细信息，请参阅 [将隔行扫描 Ddi 映射到 directdraw 和 DIRECTX VA](mapping-the-deinterlace-ddi-to-directdraw-and-directx-va.md)。

以下主题介绍了如何将 ProcAmp 控件 DDI 映射到运动补偿回调：

[用于 ProcAmp 控制的反交错容器设备](deinterlace-container-device-for-procamp-control.md)

[从用户模式组件调用 ProcAmp 控制 DDI](calling-the-procamp-control-ddi-from-a-user-mode-component.md)

 

