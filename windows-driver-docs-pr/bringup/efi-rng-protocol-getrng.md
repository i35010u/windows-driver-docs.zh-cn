---
title: EFI_RNG_PROTOCOL.GetRNG
description: EFI_RNG_PROTOCOL.GetRNG
ms.assetid: 5C2E0C8F-FF3A-4F57-BC28-3BC540852CB0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0654078e31d852be913d2325104884fe1fd7f708
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327997"
---
# <a name="efirngprotocolgetrng"></a>EFI\_RNG\_PROTOCOL.GetRNG


检索一个随机数生成 (RNG) 值。

## <a name="syntax"></a>语法


```cpp
typedef EFI_STATUS (EFIAPI *EFI_RNG_GET_RNG) (
    IN  struct _EFI_RNG_PROTOCOL    *This,
    IN  EFI_RNG_ALGORITHM           *RNGAlgorithm, OPTIONAL
    IN  UINTN                       RNGValueLength,
    OUT UINT8                       *RNGValue
    );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
\[在中\]指向的指针[EFI\_RNG\_协议](efi-rng-protocol.md)实例。

<a href="" id="rngalgorithm"></a>*RNGAlgorithm*  
\[在中\]指向 EFI\_RNG\_标识要使用的 RNG 算法的算法。 如果此参数为 NULL，则将使用默认驱动程序支持的算法。

<a href="" id="rngvaluelength"></a>*RNGValueLength*  
\[在中\]返回的缓冲区的长度，以字节为单位， *RNGValue*。

<a href="" id="rngvalue"></a>*RNGValue*  
\[在\]将包含 RNG 值的缓冲区的指针。 通过使用 EFI 此函数分配值\_引导\_服务-&gt;AllocatePool()，并且它是调用方负责释放此内存通过使用 EFI\_启动\_服务&gt;FreePool()。

## <a name="remarks"></a>备注


最小大小*RNGValue*为 32 个字节。

## <a name="return-value"></a>返回值


返回一个下面的状态代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EFI_SUCCESS</p></td>
<td><p>该函数成功返回了 RNG 值。</p></td>
</tr>
<tr class="even">
<td><p>EFI_INVALID_PARAMETER</p></td>
<td><p><em>RNGAlgorithm</em>时可使用多种算法为 NULL。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_UNSUPPORTED</p></td>
<td><p>指定的算法<em>RNGAlgorithm</em>不支持此驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>由于硬件或固件错误，无法检索 RNG 值。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_NOT_READY</p></td>
<td><p>没有足够的平均信息量数据可用。</p></td>
</tr>
<tr class="even">
<td><p>EFI_OUT_OF_RESOURCES</p></td>
<td><p>该驱动程序不能为 RNG 值分配内存。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




