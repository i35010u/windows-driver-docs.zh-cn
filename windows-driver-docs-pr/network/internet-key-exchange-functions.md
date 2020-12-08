---
title: Internet 密钥交换函数
description: 本部分介绍 Internet 密钥交换函数。
keywords:
- Internet 密钥交换功能网络驱动程序
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfb3f3bf5e37bfcbc058fd568b03e73a6ccd4794
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829489"
---
# <a name="internet-key-exchange-functions"></a>Internet 密钥交换函数

在从标注驱动程序调用时，以下函数的语义完全相同，不同之处在于，返回类型是一个 NTSTATUS 代码，而不是 Win32 错误代码。 有关每个函数的说明，请参阅 Microsoft Windows SDK 文档中的 [Windows 筛选平台](/windows/win32/fwp/windows-filtering-platform-start-page) 部分。

这些函数的调用方必须在 IRQL = PASSIVE_LEVEL 上运行。

- IkeextGetStatistics0
- IkeextSaCreateEnumHandle0
- IkeextSaDbGetSecurityInfo0
- IkeextSaDbSetSecurityInfo0
- IkeextSaDeleteById0
- IkeextSaDestroyEnumHandle0
- IkeextSaEnum0
- IkeextSaGetById0
