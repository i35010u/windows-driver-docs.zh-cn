---
title: WDI_TLV_CONFIGURED_CIPHER_KEY
description: WDI_TLV_CONFIGURED_CIPHER_KEY 是一个 TLV，其中包含要在 OID_WDI_GET_PM_PROTOCOL_OFFLOAD 中设置的已配置密码的列表。
ms.assetid: 8C7C77F7-FF62-485C-94C4-EE0F1E57D771
ms.date: 04/02/2018
keywords:
- WDI_TLV_CONFIGURED_CIPHER_KEY 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 659d6a2731bd403174beaa4e97c5540f0ec756cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844503"
---
# <a name="wdi_tlv_configured_cipher_key"></a>WDI_TLV_CONFIGURED_CIPHER_KEY

WDI_TLV_CONFIGURED_CIPHER_KEY 是一个 TLV，其中包含要在[OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)中设置的已配置密码的列表。 驱动程序必须返回当前配置的任何 GTK 或 iGTK 键。 此 TLV 是[WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) tlv 的值。

## <a name="tlv-type"></a>TLV 类型

0x147

## <a name="length"></a>长度

以下值的大小（以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| [WDI_CIPHER_KEY_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_key_type) | 正在返回的键的类型。 |
| [WDI_CIPHER_ALGORITHM](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm) | 指定使用此密钥的密码算法。 |
| UINT8\[6\] | 数据包编号（PN）的初始48位值，用于重放保护。 如果**CipherAlgorithm**为**WDI_CIPHER_ALGO_WEP40**、 **WDI_CIPHER_ALGO_WEP104**或**WDI_CIPHER_ALGO_WEP**，则为可选。 |
| TLV < LIST\<UINT8 > > | 当且仅当**CipherAlgorithm**为**WDI_CIPHER_ALGO_CCMP**时才显示。 包含 CCMP 报头密码算法密钥数据。 |
| TLV < LIST\<UINT8 > > | 当且仅当**CipherAlgorithm**为**WDI_CIPHER_ALGO_GCMP**时才显示。 包含 GCMP 密码算法密钥数据。 |
| [WDI_TLV_CIPHER_KEY_TKIP_INFO](wdi-tlv-cipher-key-tkip-info.md) | 当且仅当**CipherAlgorithm**为**WDI_CIPHER_ALGO_TKIP**时才显示。 |
| TLV < LIST\<UINT8 > > | 当且仅当**CipherAlgorithm**为**WDI_CIPHER_ALGO_BIP**时才显示。 |
| TLV < LIST\<UINT8 > > | 当且仅当**CipherAlgorithm**为**WDI_CIPHER_ALGO_WEP40**、 **WDI_CIPHER_ALGO_WEP104**或**WDI_CIPHER_ALGO_WEP**时才显示。 |
| TLV < LIST\<UINT8 > > | 当且仅当**CipherAlgorithm**在**WDI_CIPHER_ALGO_IHV_START**范围内**WDI_CIPHER_ALGO_IHV_END**时才显示。 |
 

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1803 |
| 最低受支持的服务器 | WIN ENT LTSB 2016 Finnish 64 Bits |
| 标头 | Wditypes.hpp |
