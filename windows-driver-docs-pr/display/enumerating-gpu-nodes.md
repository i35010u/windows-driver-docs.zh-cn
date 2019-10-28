---
title: 枚举 GPU 引擎功能
description: 从 Windows 8.1 开始，显示微型端口驱动程序必须实现 DxgkDdiGetNodeMetadata 函数，该函数用于查询 GPU 节点的引擎功能。
ms.assetid: 822FEB3E-A39D-4B33-BD9D-F3166EF99AF8
keywords:
- GPU 节点，枚举 WDK 显示驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be67ffb243bd76975a46c88405f02028afc6adcc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838956"
---
# <a name="enumerating-gpu-engine-capabilities"></a>枚举 GPU 引擎功能


从 Windows 8.1 开始，显示微型端口驱动程序必须实现[*DxgkDdiGetNodeMetadata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getnodemetadata)函数，该函数用于查询 GPU 节点的引擎功能。

此信息有助于评估如何在节点之间计划和分配工作负荷，并改善调试应用程序的能力。

## <a name="span-idengine_capabilities_device_driver_interface__ddi_spanspan-idengine_capabilities_device_driver_interface__ddi_spanspan-idengine_capabilities_device_driver_interface__ddi_spanengine-capabilities-device-driver-interface-ddi"></a><span id="Engine_capabilities_device_driver_interface__DDI_"></span><span id="engine_capabilities_device_driver_interface__ddi_"></span><span id="ENGINE_CAPABILITIES_DEVICE_DRIVER_INTERFACE__DDI_"></span>引擎功能设备驱动程序接口（DDI）


此接口提供指定 GPU 节点的引擎功能：

-   [*DxgkDdiGetNodeMetadata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getnodemetadata)
-   [**DXGKARG\_GETNODEMETADATA**](https://docs.microsoft.com/windows-hardware/drivers/display/)
-   [**DXGK\_引擎\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-dxgk_engine_type)

指向[*DxgkDdiGetNodeMetadata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getnodemetadata)函数的指针由驱动程序的**DxgkDdiGetNodeMetadata**成员提供[ **\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)结构。

## <a name="span-idgpu_node_architecturespanspan-idgpu_node_architecturespanspan-idgpu_node_architecturespangpu-node-architecture"></a><span id="GPU_node_architecture"></span><span id="gpu_node_architecture"></span><span id="GPU_NODE_ARCHITECTURE"></span>GPU 节点体系结构


系统上的每个显示适配器都有多个可用于计划任务的引擎。 每个引擎仅分配给一个节点，但如果该节点与多个适配器相关联，则每个节点可能包含多个引擎，例如在链接的显示适配器（LDA）配置中，多个物理 Gpu 链接起来形成单个、更快的虚拟GPU.

![gpu 引擎和节点的体系结构](images/gpu-engine-node-architecture.png)

不同的节点代表 GPU 的非对称处理核心，而每个节点中的引擎代表适配器上的对称处理核心。 也就是说，一个三维节点在多个适配器上只包含相同的3-d 引擎，而不是其他引擎类型。

由于引擎始终按引擎类型在节点中组合在一起，因此可以根据指定的节点查询引擎类型信息。 显示微型端口驱动程序可以指定的引擎类型在[**DXGK\_引擎\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-dxgk_engine_type)枚举中列出。

## <a name="span-idexample_implementation_of_node_metadata_functionspanspan-idexample_implementation_of_node_metadata_functionspanspan-idexample_implementation_of_node_metadata_functionspanexample-implementation-of-node-metadata-function"></a><span id="Example_implementation_of_node_metadata_function"></span><span id="example_implementation_of_node_metadata_function"></span><span id="EXAMPLE_IMPLEMENTATION_OF_NODE_METADATA_FUNCTION"></span>节点元数据函数的示例实现


此代码显示了显示微型端口驱动程序如何实现可由[*DxgkDdiGetNodeMetadata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getnodemetadata)函数返回的某些引擎类型。

```ManagedCPlusPlus
NTSTATUS
IHVGetNodeDescription(
        IN_CONST_HANDLE                     hAdapter,
        UINT                                NodeOrdinal,
        OUT_PDXGKARG_GETNODEMETADATA        pGetNodeMetadata
        )
{
    DDI_FUNCTION();
    PAGED_CODE();

    if(NULL == pGetNodeMetadata)
    {
        return STATUS_INVALID_PARAMETER;
    }

    CAdapter *pAdapter = GetAdapterFromHandle(hAdapter);

    //Invalid handle
    if(NULL == pAdapter)
    {
        return STATUS_INVALID_PARAMETER;
    }

    //Node ordinal is out of bounds. Required to return
    //STATUS_INVALID_PARAMETER
    if(NodeOrdinal >= pAdapter->GetNumNodes())
    {
        return STATUS_INVALID_PARAMETER;
    }

    switch(pAdapter->GetEngineType(NodeOrdinal))
    {
        //This is the adapter's 3-D engine. This engine handles a large number
        //of different workloads, but it also handles the adapter's 3-D 
        //workloads. Therefore the 3-D capability is what must be exposed.
        case GPU_ENGINE_3D:
        {
            pGetNodeMetadata->EngineType = DXGK_ENGINE_TYPE_3D;
            break;
        }

        //This is the adapter's video decoding engine
        case GPU_ENGINE_VIDEO_DECODE:
        {
            pGetNodeMetadata->EngineType = DXGK_ENGINE_TYPE_VIDEO_DECODE;
            break;
        }

        //This engine is proprietary and contains no functionality that
        //fits the DXGK_ENGINE_TYPE enumeration
        case GPU_ENGINE_PROPRIETARY_ENGINE_1:
        {
            pGetNodeMetadata->EngineType = DXGK_ENGINE_TYPE_OTHER;

            //Copy over friendly name associated with this engine
            SetFriendlyNameForEngine(pGetNodeMetadata->FriendlyName,
                                     DXGK_MAX_METADATA_NAME_LENGTH,
                                     PROPRIETARY_ENGINE_1_NAME);
            break;
        }
    }

    return STATUS_SUCCESS;
}
```

 

 





