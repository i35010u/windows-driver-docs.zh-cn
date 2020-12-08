---
title: C28735
description: 警告 C28735 禁止 Crimson API 的使用情况。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28735
ms.openlocfilehash: 31bfdaeef7a6d71e0b21f463219bf5952b827f82
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826921"
---
# <a name="c28735"></a>C28735


警告 C28735：禁止 Crimson API 使用情况

此警告表示正在使用旧事件日志或其他跟踪 API。 这些 Api 已替换为 Windows (ETW) 模型的事件跟踪，这可提高性能和安全性。 通过限制这些旧 API 调用的新用法，我们可以确保在使用事件调试 Windows 组件时，客户（尤其是管理员）可以获得最佳体验。
