---
title: WDI_TLV_CONFIGURED_CIPHER_KEY
description: WDI_TLV_CONFIGURED_CIPHER_KEY 是一种 TLV，其中包含要在 OID_WDI_GET_PM_PROTOCOL_OFFLOAD 中设置的已配置密码的列表。
ms.date: 04/02/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_CONFIGURED_CIPHER_KEY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d37b332090889caead6e4323b8dcd6a9466b71a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822743"
---
# <a name="wdi_tlv_configured_cipher_key"></a>WDI_TLV_CONFIGURED_CIPHER_KEY

WDI_TLV_CONFIGURED_CIPHER_KEY 是一种 TLV，其中包含要在 [OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)中设置的已配置密码的列表。 驱动程序必须返回当前配置的任何 GTK 或 iGTK 键。 此 TLV 是 [WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) tlv 的值。

## <a name="tlv-type"></a>TLV 类型

0x147

## <a name="length"></a>长度

以下值的大小 (以字节为单位) 。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| [WDI_CIPHER_KEY_TYPE](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_key_type) | 正在返回的键的类型。 |
| [WDI_CIPHER_ALGORITHM](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm) | 指定使用此密钥的密码算法。 |
| UINT8 \[ 6\] | 包编号 (PN) 的初始48位值，用于重放保护。 如果 **CipherAlgorithm** **WDI_CIPHER_ALGO_WEP40**、 **WDI_CIPHER_ALGO_WEP104** 或 **WDI_CIPHER_ALGO_WEP**，则为可选。 |
| TLV<列表\<UINT8>> | 当且仅当 **CipherAlgorithm** 为 **WDI_CIPHER_ALGO_CCMP** 时才显示。 包含 CCMP 报头密码算法密钥数据。 |
| TLV<列表\<UINT8>> | 当且仅当 **CipherAlgorithm** 为 **WDI_CIPHER_ALGO_GCMP** 时才显示。 包含 GCMP 密码算法密钥数据。 |
| [WDI_TLV_CIPHER_KEY_TKIP_INFO](wdi-tlv-cipher-key-tkip-info.md) | 当且仅当 **CipherAlgorithm** 为 **WDI_CIPHER_ALGO_TKIP** 时才显示。 |
| TLV<列表\<UINT8>> | 当且仅当 **CipherAlgorithm** 为 **WDI_CIPHER_ALGO_BIP** 时才显示。 |
| TLV<列表\<UINT8>> | 当且仅当 **CipherAlgorithm** 为 **WDI_CIPHER_ALGO_WEP40**、 **WDI_CIPHER_ALGO_WEP104** 或 **WDI_CIPHER_ALGO_WEP** 时才显示。 |
| TLV<列表\<UINT8>> | 当且仅当 **CipherAlgorithm** 在要 **WDI_CIPHER_ALGO_IHV_END** **WDI_CIPHER_ALGO_IHV_START** 范围内时才显示。 |
 

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1803

**支持的最低服务器**： Windows server 2016

**标头**： Wditypes. hpp
