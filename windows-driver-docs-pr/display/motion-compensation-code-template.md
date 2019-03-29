---
title: 运动补偿代码模板
description: 运动补偿代码模板
ms.assetid: 2632f84d-7ebb-4c55-9ba7-996f0cb891bd
keywords:
- 运动补偿代码模板 WDK DirectX VA
- ProcAmp WDK DirectX va，因此运动补偿代码模板
- 取消隔行扫描 WDK DirectX va，因此运动补偿代码模板
- COPP WDK DirectX va，因此运动补偿代码模板
- 复制保护 WDK COPP，运动补偿代码模板
- 视频复制保护 WDK COPP，运动补偿代码模板
- 受保护视频 WDK COPP，运动补偿代码模板
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1130c01796ab6bafc43c7a775df37a4983b4f29a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564021"
---
# <a name="motion-compensation-code-template"></a>运动补偿代码模板


## <span id="ddk_motion_compensation_code_template_gg"></span><span id="DDK_MOTION_COMPENSATION_CODE_TEMPLATE_GG"></span>


本部分中提供的代码示例演示一种实现[运动补偿](motion-compensation-callbacks.md)用于访问 ProcAmp 控件、 去隔行和认证的输出保护协议 (COPP) 功能的代码模板。 使用此模板可以简化显示驱动程序开发。 但是，不需要显示驱动程序才能正常工作的这种方式实现对 ProcAmp 控件、 去隔行和 COPP 功能的访问。

如果您的驱动程序支持其他 DirectX VA 函数，如解码 mpeg-2 视频流，然后将扩展的示例代码以包括其他 DirectX VA Guid 的处理。

本部分包括：

[定义 DirectX VA 设备类](defining-directx-va-device-classes.md)

[检索 DirectX VA 设备](retrieving-directx-va-devices.md)

[创建 DirectX VA 设备对象的实例](creating-instances-of-directx-va-device-objects.md)

[执行 ProcAmp 控制和去隔行操作](performing-procamp-control-and-deinterlacing-operations.md)

[执行去隔行与子流复合操作](performing-deinterlacing-with-substream-compositing-operations.md)

[执行 COPP 操作](performing-copp-operations-example.md)

[正在删除 DirectX VA 设备对象的实例](deleting-instances-of-directx-va-device-objects.md)

 

 





