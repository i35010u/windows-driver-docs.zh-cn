---
title: 内核安全支持例程
description: 内核安全支持例程
ms.assetid: d8ee86dc-8327-4c0b-b916-cc6763d87178
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7d5b2240ff0cad8ed5f13beac398525624baa39e
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955777"
---
# <a name="kernel-security-support-routines"></a>内核安全支持例程

以下系统提供的内核安全驱动程序（KSECDD）提供的核心安全支持例程。SYS）可由内核模式文件系统和文件系统（微筛选器和旧版）筛选器驱动程序使用。

**头文件：** *ntifs*

**Prefix：Sec @ no__t-0_Xxx_

| 函数或宏 | 描述 |
| ----------------- | ----------- |
| **SecLookupAccountName** | 接受一个帐户作为输入，并检索帐户的安全标识符（SID）和在其上找到该帐户的域的名称。 |
| **SecLookupAccountSid** | 接受安全标识符（SID）作为输入。 它会检索该 SID 的帐户名称以及在其上找到此 SID 的第一个域的名称。 |
| **SecLookupWellKnownSid** | 接受众所周知的安全标识符（SID）类型作为输入，并检索此众所周知 SID 的本地安全标识符（SID）。 |
| **SecMakeSPN** | 创建可在与特定安全服务提供程序通信时使用的服务提供程序名称字符串。 |
| **SecMakeSPNEx** | 创建可在与特定安全服务提供程序通信时使用的服务提供程序名称字符串。 |
| **SecMakeSPNEx2** | 创建可在与特定安全服务提供程序通信时使用的服务提供程序名称字符串。 |
