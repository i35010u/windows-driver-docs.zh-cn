---
title: 运动补偿代码模板
description: 运动补偿代码模板
keywords:
- 动作-补偿代码模板 WDK DirectX VA
- ProcAmp WDK DirectX VA，运动-补偿代码模板
- 取消隔行扫描 WDK DirectX VA，运动-补偿代码模板
- COPP WDK DirectX VA，运动-补偿代码模板
- 复制保护 WDK COPP，运动-补偿代码模板
- 视频复制保护 WDK COPP，运动-补偿代码模板
- 受保护的视频 WDK COPP，运动补偿代码模板
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8be4408298ab6b9656c0db4aa4b7b19232873ad5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832385"
---
# <a name="motion-compensation-code-template"></a>运动补偿代码模板


## <span id="ddk_motion_compensation_code_template_gg"></span><span id="DDK_MOTION_COMPENSATION_CODE_TEMPLATE_GG"></span>


本部分中提供的示例代码演示了一个 [运动补偿](motion-compensation-callbacks.md) 代码模板的实现，该模板用于访问 ProcAmp 控制、取消隔行扫描和认证的输出保护协议 (COPP) 功能。 使用此模板可以简化显示器驱动程序的开发。 但是，你无需以这种方式实现对 ProcAmp control、取消隔行扫描和 COPP 功能的访问，这样你的显示驱动程序就能正常工作。

如果驱动程序支持其他 DirectX VA 函数（如解码 MPEG-2 视频流），则扩展示例代码，使其包括处理额外的 DirectX VA Guid。

本节包括：

[定义 DirectX VA 设备类](defining-directx-va-device-classes.md)

[检索 DirectX VA 设备](retrieving-directx-va-devices.md)

[创建 DirectX VA 设备对象的实例](creating-instances-of-directx-va-device-objects.md)

[执行 ProcAmp 控制和反交错操作](performing-procamp-control-and-deinterlacing-operations.md)

[执行反交错与子流复合操作](performing-deinterlacing-with-substream-compositing-operations.md)

[执行 COPP 操作](performing-copp-operations-example.md)

[删除 DirectX VA 设备对象的实例](deleting-instances-of-directx-va-device-objects.md)

 

 





