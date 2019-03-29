---
title: C28735
description: 警告 C28735 禁止的 Crimson API 用法。
ms.assetid: c6cffd10-f647-4499-8f67-dfa88510d717
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28735
ms.openlocfilehash: 9a96457dd19b34f87dcd9d156cf27f7b681d533d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563754"
---
# <a name="c28735"></a>C28735


警告 C28735:已禁止的 Crimson API 用法

此警告指示正在使用旧的事件日志或其他跟踪 API。 这些 Api 已替换为事件跟踪 Windows (ETW) 模型，从而提高性能和安全性。 通过限制这些旧的 API 调用的新用途，我们确保我们的客户，尤其是管理员，有可能的最佳体验，调试 Windows 组件使用事件时。
