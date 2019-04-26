---
title: EFI_RNG_PROTOCOL.GetInfo
description: EFI_RNG_PROTOCOL.GetInfo
ms.assetid: 11E9927B-8BC6-4B01-A12D-C75B636E3988
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5a73e42b9de694807312a0e018185969bfd512a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328003"
---
# <a name="efirngprotocolgetinfo"></a>EFI\_RNG\_PROTOCOL.GetInfo


返回有关 RNG 算法实现 EFI 驱动程序支持的信息\_RNG\_协议。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI *EFI_RNG_GET_INFO) (
    IN  struct _EFI_RNG_PROTOCOL    *This,
    IN  OUT UINTN                   *RNGAlgorithmListSize,
    OUT EFI_RNG_ALGORITHM           *RNGAlgorithmList
    );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
\[在中\]指向的指针[EFI\_RNG\_协议](efi-rng-protocol.md)实例。

<a href="" id="rngalgorithmlistsize"></a>*RNGAlgorithmListSize*  
\[in、 out\]中的算法数量*RNGAlgorithmList*。

<a href="" id="rngalgorithmlist"></a>*RNGAlgorithmList*  
\[out\]指向的列表的指针[EFI\_RNG\_算法](efi-display-power-state.md)表示 RNG 算法的值。 每种算法是`sizeof(EFI_GUID)`字节长。

## <a name="remarks"></a>备注


驱动程序实现 EFI\_RNG\_协议可以支持一个或多个 RNG 算法。

返回的值*RNGAlgorithmList*参数必须在相同的驱动程序对多个调用之间更改。 在列表中的第一个算法是驱动程序的默认算法。

通过使用 EFI 此函数分配算法的列表\_引导\_服务-&gt;AllocatePool()，并且它是调用方负责释放此列表通过使用 EFI\_启动\_服务&gt;FreePool()。

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
<td><p>该函数已成功检索 RNG 算法的列表。</p></td>
</tr>
<tr class="even">
<td><p>EFI_UNSUPPORTED</p></td>
<td><p>此驱动程序不支持服务。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>由于硬件或固件错误，无法检索 RNG 算法的列表。</p></td>
</tr>
<tr class="even">
<td><p>EFI_OUT_OF_RESOURCES</p></td>
<td><p>该驱动程序将无法分配内存<em>RNGAlgorithmList</em>参数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




