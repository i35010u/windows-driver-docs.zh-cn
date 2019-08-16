---
title: 选择驱动程序模型
description: Microsoft Windows 提供了多种驱动程序模型，你可以使用这些模型编写驱动程序。
ms.assetid: 67de6453-969e-4b4d-a72e-de132b20b022
keywords:
- 驱动程序模型
- 驱动程序设计
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd9c1e5138295c5f49d8e5c9a559c3ebe37ea4c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371972"
---
# <a name="choosing-a-driver-model"></a>选择驱动程序模型


Microsoft Windows 提供了多种驱动程序模型，你可以使用这些模型编写驱动程序。 最佳驱动程序模型的选择策略取决于你计划编写的驱动程序类型。 选项如下：

-   设备函数驱动程序
-   设备筛选器驱动程序
-   软件驱动程序
-   文件系统筛选器驱动程序
-   文件系统驱动程序

有关各种类型驱动程序之间差异的介绍，请参阅[什么是驱动程序？](what-is-a-driver-.md)和[设备节点和设备堆栈](device-nodes-and-device-stacks.md)。 以下部分说明了如何为每种类型的驱动程序选择模型。

## <a name="span-idchoosing_a_driver_model_for_a_device_function_driverspanspan-idchoosing_a_driver_model_for_a_device_function_driverspanchoosing-a-driver-model-for-a-device-function-driver"></a><span id="choosing_a_driver_model_for_a_device_function_driver"></span><span id="CHOOSING_A_DRIVER_MODEL_FOR_A_DEVICE_FUNCTION_DRIVER"></span>为设备函数驱动程序选择驱动程序模型


当你设计一个硬件设备时，首先要考虑的事项之一就是你是否需要编写函数驱动程序。 提出下列问题：

是否可以完全避免编写驱动程序？
如果必须编写函数驱动程序，则最好使用哪个驱动程序模型？
若要回答这些问题，请确定设备的何处可以容纳[设备和驱动程序技术](https://docs.microsoft.com/windows-hardware/drivers/device-and-driver-technologies)中介绍的技术列表。 参阅该特定技术的文档，以确定是否需要编写函数驱动程序以及了解哪些驱动程序模型可供设备使用。

某些个别技术具有微型驱动程序模型。 在微型驱动程序模型中，设备驱动程序由两个部分组成：一个部分处理常规任务，另一部分处理设备特定的任务。 通常，Microsoft 编写通用部分，设备制造商编写设备特定的部分。 设备特定的部分具有多种名称，其中大部分名称都共享前缀“微型”  。 以下是微型驱动程序模型中使用的一些名称：

-   显示器微型端口驱动程序
-   音频微型端口驱动程序
-   电池微型类驱动程序
-   蓝牙协议驱动程序
-   HID 微型驱动程序
-   WIA 微型驱动程序
-   NDIS 微型端口驱动程序
-   存储器微型端口驱动程序
-   流微型驱动程序

有关微型驱动程序模型的概述，请参阅[微型驱动程序和驱动程序对](minidrivers-and-driver-pairs.md)。

并非[设备和驱动程序技术](https://docs.microsoft.com/windows-hardware/drivers/device-and-driver-technologies)中列出的每项技术都有专用的微型驱动程序模型。 特定技术的文档可能会建议你使用[内核模式驱动程序框架 (KMDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/)；其他技术的文档可能会建议你使用[用户模式驱动程序框架 (UMDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/)。 关键点是你应从研究特定设备技术的文档开始。 如果你的设备技术具有微型驱动程序模型，则必须使用微型驱动程序模型。 否则就遵循技术特定的文档中有关是使用 UMDF、KMDF 还是 Windows 驱动程序模型 (WDM) 的建议。

## <a name="span-idchoosing_a_driver_model_for_a_device_filter_driverspanspan-idchoosing_a_driver_model_for_a_device_filter_driverspanspan-idchoosing_a_driver_model_for_a_device_filter_driverspanchoosing-a-driver-model-for-a-device-filter-driver"></a><span id="Choosing_a_driver_model_for_a_device_filter_driver"></span><span id="choosing_a_driver_model_for_a_device_filter_driver"></span><span id="CHOOSING_A_DRIVER_MODEL_FOR_A_DEVICE_FILTER_DRIVER"></span>为设备筛选器驱动程序选择驱动程序模型


一些驱动程序频繁参与单个 I/O 请求（如从设备读取数据）。 驱动程序在堆栈中进行分层，并且可视化堆栈的常规方法是将第一个驱动程序放在顶部，将最后一个驱动程序放在底部。 堆栈具有一个函数驱动程序并且还可以具有筛选器驱动程序。 有关函数驱动程序和筛选器驱动程序的介绍，请参阅[什么是驱动程序？](what-is-a-driver-.md)和[设备节点和设备堆栈](device-nodes-and-device-stacks.md)。

如果你准备为设备编写筛选器驱动程序，则确定设备的何处可以容纳[设备和驱动程序技术](https://docs.microsoft.com/windows-hardware/drivers/device-and-driver-technologies)中介绍的技术列表。 查看特定设备技术的文档是否有关于选择筛选器驱动程序模型的任何指南。 如果设备技术的文档未提供此指南，则首先考虑使用 UMDF 作为驱动程序模型。 如果筛选器驱动程序需要访问的数据结构无法通过 UMDF 获取，则考虑使用 KMDF 作为驱动程序模型。 在极端少见的情形中，驱动程序需要访问的数据结构无法通过 KMDF 获取，则使用 WDM 作为驱动程序模型。

## <a name="span-idchoosing_a_driver_model_for_a_software_driverspanspan-idchoosing_a_driver_model_for_a_software_driverspanspan-idchoosing_a_driver_model_for_a_software_driverspanchoosing-a-driver-model-for-a-software-driver"></a><span id="Choosing_a_driver_model_for_a_software_driver"></span><span id="choosing_a_driver_model_for_a_software_driver"></span><span id="CHOOSING_A_DRIVER_MODEL_FOR_A_SOFTWARE_DRIVER"></span>为软件驱动程序选择驱动程序模型


未与设备关联的驱动程序称为“软件驱动程序”  。 有关软件驱动程序的介绍，请参阅[什么是驱动程序？](what-is-a-driver-.md)主题。 软件驱动程序很有用，原因是这些驱动程序可以在内核模式下运行，这样为其提供了受保护操作系统数据的访问权限。 有关处理器模式的信息，请参阅[用户模式和内核模式](user-mode-and-kernel-mode.md)。

对于软件驱动程序，可以使用两个选项：KMDF，以及传统的 Windows NT 驱动程序模型。 使用 KMDF 和传统 Windows NT 模型可以编写驱动程序，而无需考虑即插即用 (PnP) 和电源管理。 你可以改为专心于驱动程序的首要任务上。 使用 KMDF，你不必考虑 PnP 和电源，因为框架会为你处理 PnP 和电源。 如果使用传统 Windows NT 模型，无需考虑 PnP 和电源，因为内核模式服务在与 PnP 和电源管理完全无关的环境中运行。

我们的建议是使用 KMDF，尤其是当你已熟悉它时。 如果你希望驱动程序与 PnP 和电源管理完全无关，请使用传统 Windows NT 模型。 如果需要编写考虑电源转换或 PnP 事件的软件，则不能使用传统 Windows NT 模型，而必须使用 KMDF。

**注意**  在极少数情况下，你需要编写注意到 PnP 或电源事件的软件驱动程序，并且驱动程序需要访问无法通过 KMDF 获取的数据，你必须使用 WDM。

## <a name="span-idchoosing_a_driver_model_for_a_file_system_driverspanspan-idchoosing_a_driver_model_for_a_file_system_driverspanspan-idchoosing_a_driver_model_for_a_file_system_driverspanchoosing-a-driver-model-for-a-file-system-driver"></a><span id="Choosing_a_driver_model_for_a_file_system_driver"></span><span id="choosing_a_driver_model_for_a_file_system_driver"></span><span id="CHOOSING_A_DRIVER_MODEL_FOR_A_FILE_SYSTEM_DRIVER"></span>为文件系统驱动程序选择驱动程序模型


有关为文件系统筛选器驱动程序选择模型的帮助，请参阅[文件系统驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/samples/file-system-driver-samples)。 请注意，文件系统驱动程序非常复杂，需要具备高级驱动程序开发概念的知识。


## <a name="span-idchoosing_a_driver_model_for_a_file_system_filter_driverspanspan-idchoosing_a_driver_model_for_a_file_system_filter_driverspanspan-idchoosing_a_driver_model_for_a_file_system_filter_driverspanchoosing-a-driver-model-for-a-file-system-filter-driver"></a><span id="Choosing_a_driver_model_for_a_file_system_filter_driver"></span><span id="choosing_a_driver_model_for_a_file_system_filter_driver"></span><span id="CHOOSING_A_DRIVER_MODEL_FOR_A_FILE_SYSTEM_FILTER_DRIVER"></span>为文件系统筛选器驱动程序选择驱动程序模型


有关为文件系统筛选器驱动程序选择模型的帮助，请参阅“文件系统微过滤驱动程序”和[文件系统筛选器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ifs/file-system-filter-drivers)。

## <a name="span-idchoosing_a_driver_model_for_a_file_system_minifilter_driverspanspan-idchoosing_a_driver_model_for_a_file_system_minifilter_driverspanspan-idchoosing_a_driver_model_for_a_file_system_minifilter_driverspanchoosing-a-driver-model-for-a-file-system-minifilter-driver"></a><span id="Choosing_a_driver_model_for_a_file_system_minifilter_driver"></span><span id="choosing_a_driver_model_for_a_file_system_minifilter_driver"></span><span id="CHOOSING_A_DRIVER_MODEL_FOR_A_FILE_SYSTEM_MINIFILTER_DRIVER"></span>为文件系统微过滤驱动程序选择驱动程序模型


有关为文件系统微过滤驱动程序选择模型的帮助，请参阅[文件系统微过滤驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ifs/file-system-minifilter-drivers)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

[用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

 

 






