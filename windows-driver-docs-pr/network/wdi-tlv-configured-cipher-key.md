---
title: WDI_TLV_CONFIGURED_CIPHER_KEY
description: WDI_TLV_CONFIGURED_CIPHER_KEY 是包含一系列配置密码设置中 OID_WDI_GET_PM_PROTOCOL_OFFLOAD TLV。
ms.assetid: 8C7C77F7-FF62-485C-94C4-EE0F1E57D771
ms.date: 04/02/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_CONFIGURED_CIPHER_KEY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3a568784b252013a5f7a803612755c176087f2c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520613"
---
# <a name="wditlvconfiguredcipherkey"></a>WDI_TLV_CONFIGURED_CIPHER_KEY

WDI_TLV_CONFIGURED_CIPHER_KEY 是包含的配置中设置的密码列表 TLV [OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)。 驱动程序必须返回当前配置的任何 GTK 或 iGTK 键。 值的此 TLV 处于[WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) TLV。

## <a name="tlv-type"></a>TLV 类型

0x147

## <a name="length"></a>长度

以下值的大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| [WDI_CIPHER_KEY_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_key_type) | 要返回的项的类型。 |
| [WDI_CIPHER_ALGORITHM](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm) | 指定使用此密钥的密码算法。 |
| UINT8\[6\] | 初始 48 位值的数据包数 (PN)，用于进行重播保护。 可选如果**CipherAlgorithm**是**WDI_CIPHER_ALGO_WEP40**， **WDI_CIPHER_ALGO_WEP104**，或者**WDI_CIPHER_ALGO_WEP**。 |
| TLV<LIST\<UINT8>> | 存在当且仅当**CipherAlgorithm**是**WDI_CIPHER_ALGO_CCMP**。 包含 CCMP 密码算法的密钥数据。 |
| TLV<LIST\<UINT8>> | 存在当且仅当**CipherAlgorithm**是**WDI_CIPHER_ALGO_GCMP**。 包含 GCMP 密码算法的密钥数据。 |
| [WDI_TLV_CIPHER_KEY_TKIP_INFO](wdi-tlv-cipher-key-tkip-info.md) | 存在当且仅当**CipherAlgorithm**是**WDI_CIPHER_ALGO_TKIP**。 |
| TLV<LIST\<UINT8>> | 存在当且仅当**CipherAlgorithm**是**WDI_CIPHER_ALGO_BIP**。 |
| TLV<LIST\<UINT8>> | 存在当且仅当**CipherAlgorithm**是**WDI_CIPHER_ALGO_WEP40**， **WDI_CIPHER_ALGO_WEP104**，或者**WDI_CIPHER_ALGO_WEP**。 |
| TLV<LIST\<UINT8>> | 存在当且仅当**CipherAlgorithm**位于范围内**WDI_CIPHER_ALGO_IHV_START**到**WDI_CIPHER_ALGO_IHV_END**。 |
 

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1803 |
| 最低受支持的服务器 | Windows Server 2016 |
| 标头 | Wditypes.hpp |
