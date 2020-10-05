---
title: IPsec 函数
description: 本部分介绍适用于 Windows 筛选平台标注驱动程序的 IPsec 功能。
ms.assetid: c457f036-84be-47fd-8cfe-9ac867111ca5
keywords:
- IPsec 函数网络驱动程序
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c3da12de2c7a6c07e8f8d3f1e0e906870c3235d
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734433"
---
# <a name="ipsec-functions"></a>IPsec 函数

在从标注驱动程序调用时，以下函数的语义完全相同，不同之处在于，返回类型是一个 NTSTATUS 代码，而不是 Win32 错误代码。 有关每个函数的说明，请参阅 Microsoft Windows SDK 文档中的 [Windows 筛选平台](/windows/win32/fwp/windows-filtering-platform-start-page) 部分。

这些函数的调用方必须在 IRQL = PASSIVE_LEVEL 上运行。

- FwpmIPsecTunnelAdd0
- FwpmIPsecTunnelDeleteByKey0
- IPsecGetStatistics0
- IPsecSaContextAddInbound0
- IPsecSaContextAddOutbound0
- IPsecSaContextCreate0
- IPsecSaContextCreateEnumHandle0
- IPsecSaContextDeleteById0
- IPsecSaContextDestroyEnumHandle0
- IPsecSaContextEnum0
- IPsecSaContextExpire0
- IPsecSaContextGetById0
- IPsecSaContextGetSpi0
- IPsecSaCreateEnumHandle0
- IPsecSaDbGetSecurityInfo0
- IPsecSaDbSetSecurityInfo0
- IPsecSaDestroyEnumHandle0
- IPsecSaEnum0