---
title: IPsec 函数
description: 本部分介绍 Windows 筛选平台标注驱动程序的 IPsec 函数。
ms.assetid: c457f036-84be-47fd-8cfe-9ac867111ca5
keywords:
- IPsec 函数网络驱动程序
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ec18b25dfa268ac1762e95856ccc611fabc0961
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327695"
---
# <a name="ipsec-functions"></a>IPsec 函数

以下函数的语义是完全相同，但返回类型而不是 Win32 错误代码的 NTSTATUS 代码从用户模式应用程序中调用时从标注驱动程序，因为调用时。 每个函数的说明，请参阅[Windows 筛选平台](https://go.microsoft.com/fwlink/p/?linkid=210226)Microsoft Windows SDK 文档中的部分。

这些函数的调用方必须运行在 IRQL = passive_level 调用。

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

