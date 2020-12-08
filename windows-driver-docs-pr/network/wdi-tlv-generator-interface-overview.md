---
title: WDI TLV 生成器接口概述
description: 本部分介绍 WDI TLV 生成器接口的函数模型的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa2c265e5b39e98bfd63e2611827d34b0567b60c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792111"
---
# <a name="wdi-tlv-generator-interface-overview"></a>WDI TLV 生成器接口概述


## <a name="c-overloaded-function-model"></a>C + + 重载函数模型


在此模型中，只有一个函数调用可从数据结构生成一个 TLV 字节数组。

```c++
WDI_INDICATION_BSS_ENTRY_LIST_PARAMETERS BssEntryList = ...;
BYTE* pOutput = NULL;
ULONG length = 0;
NDIS_STATUS ndisStatus = NDIS_STATUS_SUCCESS;

ndisStatus = Generate(
    &BssEntryList,
    cbHeaderLength,
    &Context,
    &length,
    &pOutput);
```

第二个参数非常有用。 有时，TLV 缓冲区打包到更大的数据结构中，此参数允许您在该标头的缓冲区开头预保留空间。 通常， *cbHeaderLength* 的值是正确的 `sizeof(WDI_MESSAGE_HEADER)` 。

对于没有关联数据的消息，仍会重载生成 Api，但第一个参数是可选的，并且可能只是作为传入 `(EmptyMessageStructureType*)NULL` 。

完成 *pOutput* 中包含的 TLV 数据后，必须回调到库以释放缓冲区。

```c++
    FreeGenerated(pOutput);
    pOutput = NULL;
```

## <a name="c-style-function-model"></a>C 样式函数模型


在此模型中，每个顶级消息或结构都有一个特定的生成例程，因为 C 不支持重载函数。 否则，其行为与 c + + 模型相同。

```c
ndisStatus = GenerateWdiGetAdapterCapabilities(
    &adapterCapabilities,
    (ULONG)sizeof(WFC_COMMAND_HEADER),
    &Context,
    &length,
    &pOutput);
```

完成 TLV 字节数组后，回调以按照与 c + + 模型相同的方式释放内存。

```c
    FreeGenerated(pOutput);
    pOutput = NULL;
```

 

 





