---
title: 枚举 GPU 引擎功能
description: 从 Windows 8.1，显示微型端口驱动程序必须实现 DxgkDdiGetNodeMetadata 函数用于查询引擎功能的 GPU 的节点。
ms.assetid: 822FEB3E-A39D-4B33-BD9D-F3166EF99AF8
keywords:
- GPU 节点，枚举 WDK 显示器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 448e1d347a6252e1197e4304eb6afebafadd22b8
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349456"
---
# <a name="enumerating-gpu-engine-capabilities"></a>枚举 GPU 引擎功能


从 Windows 8.1，则显示微型端口驱动程序必须实现[ *DxgkDdiGetNodeMetadata* ](https://msdn.microsoft.com/library/windows/hardware/dn265415)函数，用于查询引擎功能的 GPU 的节点。

此信息可帮助使用如何计划和在节点之间分发工作负荷的评估，并改进了调试的应用程序的功能。

## <a name="span-idenginecapabilitiesdevicedriverinterfaceddispanspan-idenginecapabilitiesdevicedriverinterfaceddispanspan-idenginecapabilitiesdevicedriverinterfaceddispanengine-capabilities-device-driver-interface-ddi"></a><span id="Engine_capabilities_device_driver_interface__DDI_"></span><span id="engine_capabilities_device_driver_interface__ddi_"></span><span id="ENGINE_CAPABILITIES_DEVICE_DRIVER_INTERFACE__DDI_"></span>引擎功能设备驱动程序接口 (DDI)


此接口提供了指定的 GPU 节点的引擎功能：

-   [*DxgkDdiGetNodeMetadata*](https://msdn.microsoft.com/library/windows/hardware/dn265415)
-   [**DXGKARG\_GETNODEMETADATA**](https://msdn.microsoft.com/library/windows/hardware/dn265405)
-   [**DXGK\_ENGINE\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/dn265417)

一个指向[ *DxgkDdiGetNodeMetadata* ](https://msdn.microsoft.com/library/windows/hardware/dn265415)函数将由**DxgkDdiGetNodeMetadata**的成员[**驱动程序\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff556169)结构。

## <a name="span-idgpunodearchitecturespanspan-idgpunodearchitecturespanspan-idgpunodearchitecturespangpu-node-architecture"></a><span id="GPU_node_architecture"></span><span id="gpu_node_architecture"></span><span id="GPU_NODE_ARCHITECTURE"></span>GPU 节点体系结构


在系统上每个显示适配器具有大量不同的引擎可用于计划任务上。 每个引擎被分配到只有一个节点，但如果该节点具有多个适配器相关联，每个节点可能包含多个引擎 — 如链接的显示适配器 (LDA) 配置，其中多个物理 Gpu 链接起来以形成单个，更快、 虚拟GPU。

![gpu 引擎和节点的体系结构](images/gpu-engine-node-architecture.png)

不同节点表示 GPU 的非对称处理内核，而每个节点中的引擎适配器跨表示对称处理内核。 它是三维节点包含仅相同三维引擎上几个适配器，而绝不会不同的引擎类型。

因为引擎始终组合在一起的节点在引擎类型，可以基于指定的节点上查询引擎类型信息。 中列出了可以指定显示微型端口驱动程序的引擎的类型[ **DXGK\_引擎\_类型**](https://msdn.microsoft.com/library/windows/hardware/dn265417)枚举。

## <a name="span-idexampleimplementationofnodemetadatafunctionspanspan-idexampleimplementationofnodemetadatafunctionspanspan-idexampleimplementationofnodemetadatafunctionspanexample-implementation-of-node-metadata-function"></a><span id="Example_implementation_of_node_metadata_function"></span><span id="example_implementation_of_node_metadata_function"></span><span id="EXAMPLE_IMPLEMENTATION_OF_NODE_METADATA_FUNCTION"></span>节点的元数据函数的实现示例


此代码演示如何显示微型端口驱动程序可以实现可以返回的引擎类型的某些[ *DxgkDdiGetNodeMetadata* ](https://msdn.microsoft.com/library/windows/hardware/dn265415)函数。

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

 

 





