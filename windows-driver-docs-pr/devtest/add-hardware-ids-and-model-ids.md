---
title: 在创作向导的设备元数据中添加硬件和模型 Id
description: 在创作向导的设备元数据中添加硬件和模型 Id
ms.assetid: 1BF563AE-B37B-4105-BA76-2D13F88B2BBD
keywords:
- 在创作向导的设备元数据中添加硬件和模型 Id
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e77e7073e38b0cd567b058fe8e11b30803f30aa2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522627"
---
# <a name="add-hardware-and-model-ids-in-the-device-metadata-authoring-wizard"></a>在创作向导的设备元数据中添加硬件和模型 Id


硬件 Id 确定硬件函数基于特定于总线的值，并可用于将设备驱动程序映射到设备。 例如，具有相同的硬件 ID 的两个设备共享相同的驱动程序使用的功能接口。 硬件 Id 用于将设备元数据包映射到特定的总线或接口上的设备实例。

模型 Id 允许原始设备制造商 (OEM) 或独立硬件供应商 (IHV) 来唯一标识的总线或接口技术独立的物理设备。 例如，具有不同的模型 Id 的两个设备可能有其组件的相同硬件 Id。 模型 Id 用于将设备元数据包映射到物理设备，而不考虑如何将设备连接到计算机。

若要在设备元数据包，将关联的硬件 Id 和模型 Id，请单击**关联**选项卡。

### <a name="span-idtoaddahardwareidspanspan-idtoaddahardwareidspanspan-idtoaddahardwareidspanto-add-a-hardware-id"></a><span id="To_add_a_Hardware_ID_"></span><span id="to_add_a_hardware_id_"></span><span id="TO_ADD_A_HARDWARE_ID_"></span>若要添加的硬件 ID

1.  单击**关联**选项卡。
2.  下一步**硬件 ID**，单击**加号 （+）**。
3.  在显示的框，输入硬件 id。
    **请注意**  如果可能，使用一个值，包含你公司的供应商 id。 例如：USB\\VID\_045E&PID\_0047

     

4.  单击“确定” 。

### <a name="span-idtoaddamodelidspanspan-idtoaddamodelidspanspan-idtoaddamodelidspanto-add-a-model-id"></a><span id="To_add_a_Model_ID_"></span><span id="to_add_a_model_id_"></span><span id="TO_ADD_A_MODEL_ID_"></span>若要添加模型 ID

1.  单击**关联**选项卡。
2.  下一步**模型 ID**，单击**加号 （+）**。
3.  在显示的框，输入模型 id。 输入的 GUID 值
4.  单击“确定” 。

有关每个设备样式硬件 ID 的详细信息，请参阅[元数据包架构引用 Windows 8 设备](https://go.microsoft.com/fwlink/p/?LinkId=226753)。

 

 





