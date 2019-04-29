---
title: Windows 内核模式安全引用监视器
description: Windows 内核模式安全引用监视器
ms.assetid: 80c63d9c-cb8e-47c0-8afd-ca78dbc43327
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 448bdab0b8278cb5816d60b24d1d9437994bc45c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379355"
---
# <a name="windows-kernel-mode-security-reference-monitor"></a>Windows 内核模式安全引用监视器


操作系统的一个变得越来越重要方面是安全。 操作发生之前，操作系统必须是确认该操作不会违反系统策略。 例如，设备可能会或可能不能访问的所有请求。 在创建驱动程序时，可能想要允许某些请求是成功还是失败，具体取决于发出请求的实体的权限。

Windows 使用访问控制列表 (ACL) 来确定哪些对象具有哪些安全。 Windows 内核模式安全引用监视器提供了驱动程序以使用访问控制的例程。 有关 ACL 的详细信息，请参阅[访问控制列表](https://msdn.microsoft.com/library/windows/hardware/ff538821)。

提供安全引用 monitor direct 接口的例程都带有前缀字母"**Se**"; 例如， **SeAccessCheck**。 安全引用监视器例程的列表，请参阅[安全引用监视器例程](https://msdn.microsoft.com/library/windows/hardware/ff563711)。

 

 




