---
title: EFI_RNG_PROTOCOL.GetInfo
description: EFI_RNG_PROTOCOL.GetInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfde081297668eecb94a0ba1e0daeda4fe3df99d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789093"
---
# <a name="efi_rng_protocolgetinfo"></a>EFI \_ RNG \_ 协议。GetInfo


返回有关实现 EFI RNG 协议的驱动程序所支持的 RNG 算法的信息 \_ \_ 。

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

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
\[位于 \] [EFI \_ RNG \_ 协议](efi-rng-protocol.md) 实例的指针中。

<a href="" id="rngalgorithmlistsize"></a>*RNGAlgorithmListSize*  
\[在中，为 \] *RNGAlgorithmList* 中的算法数。

<a href="" id="rngalgorithmlist"></a>*RNGAlgorithmList*  
\[\]指向表示 RNG 算法的[EFI \_ RNG \_ 算法](efi-display-power-state.md)值列表的指针。 每个算法的 `sizeof(EFI_GUID)` 长度为个字节。

## <a name="remarks"></a>备注


实现 EFI RNG 协议的驱动程序 \_ \_ 可以支持一个或多个 RNG 算法。

*RNGAlgorithmList* 参数返回的值不能在对同一驱动程序的多个调用之间发生更改。 列表中的第一个算法是驱动程序的默认算法。

此函数使用 EFI \_ boot \_ services- &gt; AllocatePool ( # A1 分配算法的列表，调用方负责通过使用 efi \_ 启动 \_ 服务 &gt; FreePool ( # A3 来释放此列表。

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
<td><p>函数已成功检索 RNG 算法的列表。</p></td>
</tr>
<tr class="even">
<td><p>EFI_UNSUPPORTED</p></td>
<td><p>此驱动程序不支持该服务。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>由于硬件或固件错误，无法检索 RNG 算法的列表。</p></td>
</tr>
<tr class="even">
<td><p>EFI_OUT_OF_RESOURCES</p></td>
<td><p>驱动程序无法为 <em>RNGAlgorithmList</em> 参数分配内存。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




