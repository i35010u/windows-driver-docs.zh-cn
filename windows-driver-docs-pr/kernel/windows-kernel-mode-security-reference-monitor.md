---
title: Windows 内核模式安全引用监视器
description: Windows 内核模式安全引用监视器
ms.assetid: 80c63d9c-cb8e-47c0-8afd-ca78dbc43327
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cca12802c08bf3c3c4676d770bd7edbfae859831
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193073"
---
# <a name="windows-kernel-mode-security-reference-monitor"></a>Windows 内核模式安全引用监视器


操作系统的一个越来越重要的方面是安全性。 在执行某一操作之前，操作系统必须确保该操作不违反系统策略。 例如，所有请求都可能或无法访问设备。 创建驱动程序时，您可能希望允许某些请求成功或失败，具体取决于发出请求的实体的权限。

Windows 使用访问控制列表 (ACL) 来确定哪些对象具有哪些安全性。 Windows 内核模式安全参考监视器为驱动程序提供例程，使其能够使用访问控制。 有关 ACL 的详细信息，请参阅 [访问控制列表](../ifs/access-control-list.md)。

为安全引用监视器提供直接接口的例程以字母 "**Se**" 作为前缀;例如， **SeAccessCheck**。 有关安全引用监视器例程的列表，请参阅 [安全引用监视器例程](/previous-versions/windows/hardware/drivers/ff563711(v=vs.85))。

 

