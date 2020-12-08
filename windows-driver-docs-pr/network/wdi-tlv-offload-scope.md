---
title: WDI_TLV_OFFLOAD_SCOPE
description: WDI_TLV_OFFLOAD_SCOPE 是包含 Rx 合并卸载功能的 TLV。
ms.date: 10/05/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_OFFLOAD_SCOPE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 67027130e2e9fd724708ed9d7f6dd0c8ea8d3973
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821222"
---
# <a name="wdi_tlv_offload_scope"></a>WDI_TLV_OFFLOAD_SCOPE


WDI_TLV_OFFLOAD_SCOPE 为 TLV，其中包含网络卸载的作用域。

## <a name="tlv-type"></a>TLV 类型


0x143

## <a name="length"></a>长度


以下值的大小 (以字节为单位) 。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT8 | 指定校验和卸载参数是否适用于所有端口。 <p>可能的值：</p> <ul><li>0：不适用</li><li>1：适用</li></ul> |
| UINT8 | 指定 LsoV1 卸载参数是否适用于所有端口。 <p>可能的值：</p> <ul><li>0：不适用</li><li>1：适用</li></ul> |
| UINT8 | 指定 LsoV2 卸载参数是否适用于所有端口。 <p>可能的值：</p> <ul><li>0：不适用</li><li>1：适用</li></ul> |
| UINT8 | 指定 RSC 卸载参数是否适用于所有端口。 <p>可能的值：</p> <ul><li>0：不适用</li><li>1：适用</li></ul> |
 

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1709

**支持的最低服务器**： Windows server 2016

**标头**： Wditypes. hpp




