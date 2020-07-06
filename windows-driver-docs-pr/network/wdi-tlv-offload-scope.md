---
title: WDI_TLV_OFFLOAD_SCOPE
description: WDI_TLV_OFFLOAD_SCOPE 是包含 Rx 合并卸载功能的 TLV。
ms.assetid: 2E00659F-4A41-4907-AEA6-92EAFBFF2149
ms.date: 10/05/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_OFFLOAD_SCOPE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 570e0ba1bd44ba1082105347c03cb5a2b7ff4f80
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968528"
---
# <a name="wdi_tlv_offload_scope"></a>WDI_TLV_OFFLOAD_SCOPE


WDI_TLV_OFFLOAD_SCOPE 为 TLV，其中包含网络卸载的作用域。

## <a name="tlv-type"></a>TLV 类型


0x143

## <a name="length"></a>长度


以下值的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT8 | 指定校验和卸载参数是否适用于所有端口。 <p>可能的值：</p> <ul><li>0：不适用</li><li>1：适用</li></ul> |
| UINT8 | 指定 LsoV1 卸载参数是否适用于所有端口。 <p>可能的值：</p> <ul><li>0：不适用</li><li>1：适用</li></ul> |
| UINT8 | 指定 LsoV2 卸载参数是否适用于所有端口。 <p>可能的值：</p> <ul><li>0：不适用</li><li>1：适用</li></ul> |
| UINT8 | 指定 RSC 卸载参数是否适用于所有端口。 <p>可能的值：</p> <ul><li>0：不适用</li><li>1：适用</li></ul> |
 

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1709

**支持的最低服务器**： Windows server 2016

**标头**： Wditypes. hpp




