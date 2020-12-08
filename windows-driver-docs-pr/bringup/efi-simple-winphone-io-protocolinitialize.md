---
title: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Initialize
description: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Initialize
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feea6fb8861cbbb3e94ef624630ffdfe0d4249d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803397"
---
# <a name="efi_simple_winphone_io_protocolinitialize"></a>EFI \_ 简单 \_ WINPHONE \_ IO \_PROTOCOL.Initialize


**Initialize** 函数在指定的秒数内等待宿主计算机的连接。 如果未建立有效的连接，则会将 **EFI \_ 超时** 作为失败状态返回。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS(EFIAPI * EFI_SIMPLE_WINPHONE_IO_INITIALIZE) 
(
  IN EFI_SIMPLE_WINPHONE_IO_PROTOCOL    *This,
  IN UINTN                              ConnectionTimeout,
  IN UINTN                              ReadWriteTimeout
  );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI \_ 简单 \_ WINPHONE \_ IO \_ 协议实例的指针。

<a href="" id="connectiontimeout"></a>*ConnectionTimeout*  
等待主机连接的毫秒数。

<a href="" id="readwritetimeout"></a>*ReadWriteTimeout*  
等待读写操作完成的毫秒数。

## <a name="return-values"></a>返回值


该函数返回以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EFI_SUCCESS</strong></p></td>
<td><p>函数已成功返回</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_INVALID_PARAMETER</strong></p></td>
<td><p>参数无效</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_DEVICE_ERROR</strong></p></td>
<td><p>物理设备报告了一个错误。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_NOT_READY</strong></p></td>
<td><p>物理设备处于繁忙状态或尚未准备好处理此请求</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_TIMEOUT</strong></p></td>
<td><p>建立连接之前出现超时。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




