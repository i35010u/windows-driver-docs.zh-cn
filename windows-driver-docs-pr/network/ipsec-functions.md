---
title: IPsec 函数
description: 本部分介绍适用于 Windows 筛选平台标注驱动程序的 IPsec 功能。
keywords:
- IPsec 函数网络驱动程序
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 415800c5c7fa3ba24601b492ac73e4281e8a084e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789771"
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
