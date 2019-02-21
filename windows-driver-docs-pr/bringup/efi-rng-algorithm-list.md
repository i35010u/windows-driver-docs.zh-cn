---
title: EFI_RNG_ALGORITHM_LIST 结构
description: 此数据结构包含受支持的随机数字生成 (RNG) 算法的列表。
ms.assetid: 1481330F-78F3-4C18-BD19-3B4984E0138F
keywords:
- EFI_RNG_ALGORITHM_LIST 结构
- PEFI_RNG_ALGORITHM_LIST 结构指针
topic_type:
- apiref
api_name:
- EFI_RNG_ALGORITHM_LIST
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8437c21fd7e2895330f60f09798eedcb4fc55026
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541774"
---
# <a name="efirngalgorithmlist-structure"></a>EFI\_RNG\_算法\_列表结构


此数据结构包含受支持的随机数字生成 (RNG) 算法的列表。

<a name="syntax"></a>语法
------

```cpp
typedef struct _EFI_RNG_ALGORITHM_LIST {
  UINT32     AlgorithmsCount;
  EFI_GUID * Algorithms;
} EFI_RNG_ALGORITHM_LIST, *PEFI_RNG_ALGORITHM_LIST;
```

<a name="members"></a>成员
-------

**AlgorithmsCount**  
列表中的算法的数。

**算法**  
指向 RNG 算法的列表。 每种算法是`sizeof(EFI_GUID)`字节长。 它是调用方负责释放此内存通过使用 EFI\_引导\_服务-&gt;FreePool()。

<a name="remarks"></a>备注
-------

实现可能支持一个或多个方法提供 RNG 值。 在此结构中表示支持 RNG 算法的列表。

以下列表提供了 EFI GUID 值的一系列 EFI\_RNG\_协议算法。 此列表并不详尽，而且可能会通过供应商或其他行业标准来进行扩充。

```cpp
#define EFI_RNG_ALGORITHM_SP800_90_HASH_256_GUID   \
  {0xa7af67cb, 0x603b, 0x4d42, 0xba, 0x21, 0x70, 0xbf, 0xb6, 0x29,\
   0x3f, 0x96}
#define EFI_RNG_ALGORITHM_SP800_90_HMAC_256_GUID    \
  {0xc5149b43, 0xae85, 0x4f53, 0x99, 0x82, 0xb9, 0x43, 0x35, 0xd3,\
   0xa9, 0xe7}
#define EFI_RNG_ALGORITHM_SP800_90_CTR_256_GUID \
  {0x44f0de6e, 0x4d8c, 0x4045, 0xa8, 0xc7, 0x4d, 0xd1, 0x68, 0x85,\
   0x6b, 0x9e}
```
