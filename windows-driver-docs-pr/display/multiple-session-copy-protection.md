---
title: 多会话复制保护
description: 多会话复制保护
keywords:
- 复制保护 WDK 视频微型端口，多个会话
- 多个会话复制保护 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c9347a31aa0c4e943e0f52f1c0843ed7c012cb5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840385"
---
# <a name="multiple-session-copy-protection"></a>多会话复制保护


## <span id="ddk_multiple_session_copy_protection_gg"></span><span id="DDK_MULTIPLE_SESSION_COPY_PROTECTION_GG"></span>


具有复制保护的设备的微型端口驱动程序可以选择支持多个同时复制保护会话。 为此，微型端口驱动程序应执行以下操作：

-   为每个复制保护激活，返回 **dwCPKey** 中的唯一复制保护密钥。

-   保持复制保护的启用状态，直到已暂时关闭所有会话 (通过 VP \_ cp \_ cmd \_ CHANGE) 或停用 (副总裁 \_ \_ cmd cmd \_ 停用) 。 例如，微型端口驱动程序可以在每次激活复制保护时递增或递减引用计数 (VP \_ CP \_ CMD \_ ACTIVATE) 或停用/关闭，仅在引用计数为零时禁用复制保护。

 

 





