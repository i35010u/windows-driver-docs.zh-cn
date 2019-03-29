---
title: WDI TLV 生成器接口概述
description: 本部分介绍 WDI TLV 生成器接口函数模型的概述
ms.assetid: 8A344BF7-932E-4404-9B3E-E7D3C33722C3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe1a49a55ebbb1c918e011a724f64f90a9c48092
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576477"
---
# <a name="wdi-tlv-generator-interface-overview"></a>WDI TLV 生成器接口概述


## <a name="c-overloaded-function-model"></a>C + + 重载的函数模型


在此模型中，将只有一个函数调用来从您的数据结构生成 TLV 字节数组。

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

第二个参数可以是非常有帮助。 有时，TLV 缓冲区打包到更大的数据结构，此参数，可预先保留该标头的缓冲区开始处的空间。 正确的值*cbHeaderLength*通常是`sizeof(WDI_MESSAGE_HEADER)`。

对于不具有关联的数据的消息，有仍重载生成的 Api，但第一个参数是可选的可能只需传递中作为`(EmptyMessageStructureType*)NULL`。

中包含的 TLV 数据完成后*pOutput*，您必须重新调入库来释放缓冲区。

```c++
    FreeGenerated(pOutput);
    pOutput = NULL;
```

## <a name="c-style-function-model"></a>C 样式函数模型


在此模型中，每个顶级消息的特定生成例程或结构，因为 C 不支持重载函数。 否则，它的行为与 c + + 模型相同。

```c
ndisStatus = GenerateWdiGetAdapterCapabilities(
    &adapterCapabilities,
    (ULONG)sizeof(WFC_COMMAND_HEADER),
    &Context,
    &length,
    &pOutput);
```

完成 TLV 字节数组，调用返回作为 c + + 模型相同的方式释放的内存。

```c
    FreeGenerated(pOutput);
    pOutput = NULL;
```

 

 





