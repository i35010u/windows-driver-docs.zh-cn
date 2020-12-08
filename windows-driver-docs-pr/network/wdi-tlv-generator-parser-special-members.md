---
title: WDI TLV 生成器/分析器特殊成员
description: 本部分介绍 WDI TLV 生成器/分析器的特殊成员
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bc993c04aed577a4602cfd0a8eed572e78541a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817045"
---
# <a name="wdi-tlv-generatorparser-special-members"></a>WDI TLV 生成器/分析器特殊成员


## <a name="optional-members"></a>可选成员


对于具有可选子 TLV 成员的任何 TLV，父节点有一个名为 " **可选**" 的字段。 在该字段中，名为 **_&lt; child \_ name &gt;_ \_ IsPresent** 的每个可选子级都有一个布尔字段，如果子名称存在，则它将设置为 TRUE; 否则为 FALSE。 同样，如果字段应存在于 TLV 字节流中，则生成 Api 应为 TRUE，否则为 FALSE。

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


如果同一类型的多个子级出现在同一父 (（例如， &lt; 容器/ &gt; 的 *isCollection* 特性) ），则分析器和生成器将使用特殊的结构来表示数组： ArrayOfElements。 对于 c + + 客户端，这是一个强类型的模板结构，其中包含对析构语义的清理。 对于 C 客户端，会创建显式命名的结构 (例如 ArrayOfElementsOfUINT8) 。 但是，这些结构不会自动清理，因为 C 不支持析构函数，因此，C Api 的用户必须小心地不要引入内存泄漏 (或加倍) 。

ArrayOfElements 中有两个重要字段： **elementcount 多于** 和 **pElements**。 **Elementcount 多于** 是数组中元素的计数。 **pElements** 是元素的 C 样式数组。 可以循环访问元素，如本示例中所示。

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

第三个字段 **MemoryInternallyAllocated** 由分析器/生成器在内部使用。 它不应由 IHV 修改。

 

 





