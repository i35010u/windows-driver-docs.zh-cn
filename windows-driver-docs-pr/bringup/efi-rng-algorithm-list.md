---
title: EFI_RNG_ALGORITHM_LIST 结构
description: 此数据结构包含一个列表，其中列出了支持的随机数生成 (RNG) 算法。
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
ms.openlocfilehash: a89c25ce26ea5dbc6170a4f9a2102baaea353b9f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803403"
---
# <a name="efi_rng_algorithm_list-structure"></a>EFI \_ RNG \_ 算法 \_ 列表结构


此数据结构包含一个列表，其中列出了支持的随机数生成 (RNG) 算法。

<a name="syntax"></a>语法
------

```cpp
typedef struct _EFI_RNG_ALGORITHM_LIST {
  UINT32     AlgorithmsCount;
  EFI_GUID * Algorithms;
} EFI_RNG_ALGORITHM_LIST, *PEFI_RNG_ALGORITHM_LIST;
```

<a name="members"></a>成员
-------

**AlgorithmsCount**  
列表中算法的数目。

**算法**  
指向 RNG 算法列表的指针。 每个算法的 `sizeof(EFI_GUID)` 长度为个字节。 调用方负责通过使用 EFI \_ BOOT \_ SERVICES- &gt; FreePool ( # A1 来释放此内存。

<a name="remarks"></a>备注
-------

实现可支持一种或多种方法来提供 RNG 值。 此结构中表示受支持的 RNG 算法的列表。

以下列表提供了可选的 EFI \_ RNG 协议算法的 EFI GUID 值 \_ 。 此列表并不完整，并且可能会被供应商或其他行业标准所增强。

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
