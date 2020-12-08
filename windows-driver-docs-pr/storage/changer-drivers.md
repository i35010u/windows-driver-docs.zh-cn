---
title: 更换器驱动程序简介
description: 更换器驱动程序
keywords:
- 变换器驱动程序 WDK 存储
- 存储更换器驱动程序 WDK
- 存储驱动程序 WDK，更换器驱动程序
- 转换器驱动程序的 WDK 存储，关于更换器驱动程序
- 存储更换器驱动程序 WDK，关于更换器驱动程序
- 自动加载 WDK 存储
- 自动转换器 WDK 存储
- 自动存储塔 WDK 存储
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 58749d0102375df76daa100fdc0218414a3a77e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804735"
---
# <a name="introduction-to-changer-drivers"></a>更换器驱动程序简介

更换器驱动程序可控制媒体库的元素，或 *转换器* (有时称为自动换带 *机*、 *自动转换器* 或 *盘库*) 。 在基于 NT 的操作系统中，更换器的驱动程序包括以下各项：

- 系统提供的变换器类驱动程序，作为库 *mcd* 提供，它提供了所有转换器驱动程序所共有的功能

- 一种特定于设备的 miniclass 驱动程序，静态链接到 *mcd*，提供由更改器类驱动程序调用以支持特定类型的转换器的例程

本部分介绍 Windows 更换器驱动程序模型，并提供编写新的转换器 miniclass 驱动程序的详细信息。
