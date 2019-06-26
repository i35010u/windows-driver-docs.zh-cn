---
title: Windows 内核模式安全引用监视器
description: Windows 内核模式安全引用监视器
ms.assetid: 80c63d9c-cb8e-47c0-8afd-ca78dbc43327
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 042d88d320d36f0fc1300d100303d07849113f49
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386872"
---
# <a name="windows-kernel-mode-security-reference-monitor"></a>Windows 内核模式安全引用监视器


操作系统的一个变得越来越重要方面是安全。 操作发生之前，操作系统必须是确认该操作不会违反系统策略。 例如，设备可能会或可能不能访问的所有请求。 在创建驱动程序时，可能想要允许某些请求是成功还是失败，具体取决于发出请求的实体的权限。

Windows 使用访问控制列表 (ACL) 来确定哪些对象具有哪些安全。 Windows 内核模式安全引用监视器提供了驱动程序以使用访问控制的例程。 有关 ACL 的详细信息，请参阅[访问控制列表](https://docs.microsoft.com/windows-hardware/drivers/ifs/access-control-list)。

提供安全引用 monitor direct 接口的例程都带有前缀字母"**Se**"; 例如， **SeAccessCheck**。 安全引用监视器例程的列表，请参阅[安全引用监视器例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563711(v=vs.85))。

 

 




