---
title: Internet 密钥交换函数
description: 本部分介绍 Internet 密钥交换函数。
ms.assetid: 993a6db0-018c-4529-bccc-46b522e74c79
keywords:
- Internet 密钥交换函数网络驱动程序
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: b67173175b6e885c05071e2d021b47b9677f89b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522426"
---
# <a name="internet-key-exchange-functions"></a>Internet 密钥交换函数

以下函数的语义是完全相同，但返回类型而不是 Win32 错误代码的 NTSTATUS 代码从用户模式应用程序中调用时从标注驱动程序，因为调用时。 每个函数的说明，请参阅[Windows 筛选平台](https://go.microsoft.com/fwlink/p/?linkid=210226)Microsoft Windows SDK 文档中的部分。

这些函数的调用方必须运行在 IRQL = passive_level 调用。

- IkeextGetStatistics0
- IkeextSaCreateEnumHandle0
- IkeextSaDbGetSecurityInfo0
- IkeextSaDbSetSecurityInfo0
- IkeextSaDeleteById0
- IkeextSaDestroyEnumHandle0
- IkeextSaEnum0
- IkeextSaGetById0

