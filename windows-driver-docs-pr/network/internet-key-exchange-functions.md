---
title: Internet 密钥交换函数
description: 本部分介绍 Internet 密钥交换函数。
ms.assetid: 993a6db0-018c-4529-bccc-46b522e74c79
keywords:
- Internet 密钥交换功能网络驱动程序
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: b46ece8761dc12f9c11177dea0a28a05caf9d15b
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733397"
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