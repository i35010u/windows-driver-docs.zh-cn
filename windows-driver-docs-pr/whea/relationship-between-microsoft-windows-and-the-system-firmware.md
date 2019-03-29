---
title: Microsoft Windows 和系统固件之间的关系
description: Microsoft Windows 和系统固件之间的关系
ms.assetid: 83a43e49-cb06-4007-88d0-88f024c22825
keywords:
- Windows 硬件错误体系结构 WDK、 Windows 和固件
- WHEA WDK、 Windows 和固件
- WDK WHEA、 Windows 和固件硬件错误
- 错误 WDK WHEA、 Windows 和固件
- 固件 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51f8c275257ccac541203080295a9c6809e7fe00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562845"
---
# <a name="relationship-between-microsoft-windows-and-the-system-firmware"></a>Microsoft Windows 和系统固件之间的关系


Microsoft Windows 操作系统和系统固件硬件错误处理方法中扮演重要角色。 Windows 硬件错误体系结构 (WHEA) 可以提高的同时可能会导致硬件错误处理的任务的方法。 WHEA，硬件平台供应商可以确定固件或操作系统将拥有关键硬件错误的资源。 此外，使用 WHEA 固件可传递硬件错误资源的控制操作系统在适当的时候。

操作系统应拥有尽可能多的硬件错误资源切实可行的前提。 但是，系统固件必须继续管理这些资源因硬件错误资源标准化程度不足而导致的一些。 定义和采用更多的硬件错误报告标准时，Microsoft 认为可以操作系统控制下放置的硬件错误处理机制的详细信息。

 

 




