---
title: WDI TLV 生成器/分析器特殊成员
description: 本部分介绍 WDI TLV 生成器/分析器的特殊成员
ms.assetid: 2FD485E5-E2F9-4B21-A777-ABA9693B1223
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49fdbc21dac128aa40c307f0f3a2580f578e1d73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382863"
---
# <a name="wdi-tlv-generatorparser-special-members"></a>WDI TLV 生成器/分析器特殊成员


## <a name="optional-members"></a>可选的成员


对于具有可选子 TLV 成员任何 TLV，父级具有名为的一个字段**可选**。 在该字段中，没有名为每个可选子的一个布尔字段 * **&lt;子\_名称&gt;*\_IsPresent**，其设置为 TRUE 分析器如果子级在现在和 FALSE 其他方面。 同样，如果它应该位于 TLV 字节流，且 FALSE 否则，则为 TRUE Api 预期需要该字段的代。

```C++
WDI_SET_FIRMWARE_CONFIGURATION_PARAMETERS fwConfig = { 0 };
NDIS_STATUS status;
status = ParseWdiSetAdapterConfiguration(
    pNdisRequest->DATA.METHOD_INFORMATION.InputBufferLength - 
        sizeof(WDI_MESSAGE_HEADER),
    (PUINT8)pNdisRequest->DATA.METHOD_INFORMATION.InformationBuffer + 
        sizeof(WDI_MESSAGE_HEADER),
    0,
    &fwConfig);

if (status == NDIS_STATUS_SUCCESS)
{
    if (fwConfig.Optional.MacAddress_IsPresent)
    {
        // Safe to use fwConfig.MacAddress
        fwConfig.MacAddress;
    }
}
```

## <a name="array-members"></a>数组成员


相同类型的多个子级时出现在同一父级 (例如，&lt;容器 /&gt;的*isCollection*属性)，分析器和生成器使用的特殊结构来表示数组：ArrayOfElements。 有关C++客户端，这是一个强类型化的模板结构与清理析构语义。 对于 C 客户端 （例如 ArrayOfElementsOfUINT8） 创建显式命名的结构。 但是，这些结构不会自动清理因为 C 不支持析构函数，因此必须小心以免引入内存泄漏的 C Api 的用户 （或重复释放）。

有两个重要字段 ArrayOfElements 中：**ElementCount**并**pElements**。 **ElementCount**是数组中元素的计数。 **pElements**是 C 样式数组的元素。 元素可以循环访问此示例中所示。

```C++
for (UINT32 i = 0;
    i < pConnectTaskParameters->ConnectParameters.
            MulticastCipherAlgorithms.ElementCount;
    i++)
{
    // Safe to use pElements[i]
    pConnectTaskParameters->ConnectParameters.MulticastCipherAlgorithms.
        pElements[i];
}
```

第三个字段**MemoryInternallyAllocated**，分析器/生成器在内部使用。 它不应由 IHV 修改。

 

 





