---
title: EFI_RNG_PROTOCOL.GetRNG
description: EFI_RNG_PROTOCOL.GetRNG
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a7d2084af331ec61ea1b7ffe83c731617e59337
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803401"
---
# <a name="efi_rng_protocolgetrng"></a>EFI \_ RNG \_ 协议。GetRNG


 (RNG) 值检索随机数生成。

## <a name="syntax"></a>语法


```cpp
typedef EFI_STATUS (EFIAPI *EFI_RNG_GET_RNG) (
    IN  struct _EFI_RNG_PROTOCOL    *This,
    IN  EFI_RNG_ALGORITHM           *RNGAlgorithm, OPTIONAL
    IN  UINTN                       RNGValueLength,
    OUT UINT8                       *RNGValue
    );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
\[位于 \] [EFI \_ RNG \_ 协议](efi-rng-protocol.md) 实例的指针中。

<a href="" id="rngalgorithm"></a>*RNGAlgorithm*  
\[\]用于 \_ \_ 标识要使用的 RNG 算法的 EFI RNG 算法的指针。 如果此参数为 NULL，则将使用该驱动程序支持的默认算法。

<a href="" id="rngvaluelength"></a>*RNGValueLength*  
\[\] *RNGValue* 返回的缓冲区的长度（以字节为单位）。

<a href="" id="rngvalue"></a>*RNGValue*  
\[\]指向将包含 RNG 值的缓冲区的指针。 此函数使用 EFI \_ boot \_ services-AllocatePool ( # A1 为此函数分配该值 &gt; ，并且调用方负责使用 efi \_ 启动 \_ 服务 &gt; FreePool ( # A3 来释放此内存。

## <a name="remarks"></a>备注


*RNGValue* 的最小大小为32个字节。

## <a name="return-value"></a>返回值


返回以下状态代码之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EFI_SUCCESS</p></td>
<td><p>函数已成功返回 RNG 值。</p></td>
</tr>
<tr class="even">
<td><p>EFI_INVALID_PARAMETER</p></td>
<td><p>如果有多种算法， <em>RNGAlgorithm</em>为 NULL。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_UNSUPPORTED</p></td>
<td><p>此驱动程序不支持 <em>RNGAlgorithm</em> 指定的算法。</p></td>
</tr>
<tr class="even">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>由于硬件或固件错误，无法检索到 RNG 的值。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_NOT_READY</p></td>
<td><p>没有足够的熵数据可用。</p></td>
</tr>
<tr class="even">
<td><p>EFI_OUT_OF_RESOURCES</p></td>
<td><p>驱动程序无法为 RNG 值分配内存。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




