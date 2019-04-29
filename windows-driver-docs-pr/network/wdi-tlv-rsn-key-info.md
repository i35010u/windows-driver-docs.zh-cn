---
title: WDI_TLV_RSN_KEY_INFO
description: WDI_TLV_RSN_KEY_INFO 是包含 Rsn Eapol 密钥参数 TLV。
ms.assetid: 8C7C77F7-FF62-485C-94C4-EE0F1E57D771
ms.date: 04/02/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_RSN_KEY_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c86ecacd424f00a41db920352ce3bd618aa7e0ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359092"
---
# <a name="wditlvrsnkeyinfo"></a>WDI_TLV_RSN_KEY_INFO

WDI_TLV_RSN_KEY_INFO 是包含 Rsn Eapol 密钥参数 TLV。 值的此 TLV 处于[WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) TLV。

## <a name="tlv-type"></a>TLV 类型

0x148

## <a name="length"></a>长度

以下值的大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT32 | 一个 UINT32 值，指定协议卸载 id。 这是一个操作系统提供的值，标识已卸载的协议。 操作系统向下发送添加请求或对基础驱动程序的请求完成之前，为在协议中唯一值的 OS 集 ProtocolOffloadId 将卸载网络适配器上。 |
| UINT64 | 指定重播计数器 UINT64 值。 |
| UINT8\[16\] | UINT8 数组，指定 IEEE 802.11 密钥确认密钥 (KCK)。 |
| UINT8\[16\] | UINT8 数组，指定 IEEE 802.11 密钥加密密钥 (KEK)。  |
 

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1803 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
