---
title: WDI_TLV_OFFLOAD_SCOPE
description: WDI_TLV_OFFLOAD_SCOPE 是包含 Rx TLV coalesce 卸载功能。
ms.assetid: 2E00659F-4A41-4907-AEA6-92EAFBFF2149
ms.date: 10/05/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_OFFLOAD_SCOPE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 62fde916cdec2dd2a9041c67461e7a3f8f8531a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575756"
---
# <a name="wditlvoffloadscope"></a>WDI_TLV_OFFLOAD_SCOPE


WDI_TLV_OFFLOAD_SCOPE 是包含网络的作用域 TLV 将卸载。

## <a name="tlv-type"></a>TLV 类型


0x143

## <a name="length"></a>长度


大小 （以字节为单位） 的以下值。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT8 | 指定所有端口上的校验和卸载参数是否适用。 <p>可能值：</p> <ul><li>0:不适用</li><li>1：适用</li></ul> |
| UINT8 | 指定所有端口上是否适用 LsoV1 卸载参数。 <p>可能值：</p> <ul><li>0:不适用</li><li>1：适用</li></ul> |
| UINT8 | 指定所有端口上是否适用 LsoV2 卸载参数。 <p>可能值：</p> <ul><li>0:不适用</li><li>1：适用</li></ul> |
| UINT8 | 指定所有端口上是否适用 RSC 卸载参数。 <p>可能值：</p> <ul><li>0:不适用</li><li>1：适用</li></ul> |
 

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1709 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |



