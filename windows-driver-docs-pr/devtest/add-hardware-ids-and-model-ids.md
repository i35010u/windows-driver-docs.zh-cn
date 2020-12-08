---
title: 在设备元数据创作向导中添加硬件和模型 ID
description: 在设备元数据创作向导中添加硬件和模型 ID
keywords:
- 在设备元数据创作向导中添加硬件和模型 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bb9e551916b82a7802c6047883ccdd24ae0a28a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795129"
---
# <a name="add-hardware-and-model-ids-in-the-device-metadata-authoring-wizard"></a>在设备元数据创作向导中添加硬件和模型 ID


硬件 Id 基于特定于总线的值识别硬件功能，可用于将设备驱动程序映射到设备。 例如，两个具有相同硬件 ID 的设备共享同一驱动程序使用的功能接口。 硬件 Id 用于将设备元数据包映射到特定总线或接口上的设备实例。

模型 Id 允许原始设备制造商 (OEM) 或独立硬件供应商 (IHV) ，以唯一标识与总线或接口技术无关的物理设备。 例如，两个具有不同模型 Id 的设备可能为其组件具有相同的硬件 Id。 模型 Id 用于将设备元数据包映射到物理设备，无论设备连接到计算机的方式如何。

若要关联设备元数据包的硬件 Id 和型号 Id，请单击 " **关联** " 选项卡。

### <a name="span-idto_add_a_hardware_id_spanspan-idto_add_a_hardware_id_spanspan-idto_add_a_hardware_id_spanto-add-a-hardware-id"></a><span id="To_add_a_Hardware_ID_"></span><span id="to_add_a_hardware_id_"></span><span id="TO_ADD_A_HARDWARE_ID_"></span>添加硬件 ID

1.  单击 " **关联** " 选项卡。
2.  在 " **硬件 ID**" 旁边，单击 **加号 (+)**。
3.  在出现的框中，输入硬件 ID。
    **注意**  如果可能，请使用包含公司供应商 ID 的值。 例如： USB \\ VID \_ 045E&PID \_ 0047

     

4.  单击 **“确定”** 。

### <a name="span-idto_add_a_model_id_spanspan-idto_add_a_model_id_spanspan-idto_add_a_model_id_spanto-add-a-model-id"></a><span id="To_add_a_Model_ID_"></span><span id="to_add_a_model_id_"></span><span id="TO_ADD_A_MODEL_ID_"></span>添加模型 ID

1.  单击 " **关联** " 选项卡。
2.  单击 " **模型 ID**" 旁边的 **加号 (+)**。
3.  在出现的框中，输入模型 ID 的 GUID 值。
4.  单击 **“确定”** 。

有关每种设备样式的硬件 ID 的详细信息，请参阅 [设备元数据包概述](../install/overview-of-device-metadata-packages.md)。

 

