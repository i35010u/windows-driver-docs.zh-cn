---
title: Windows 打开的供系统使用的顶级集合
description: Windows 打开的供系统使用的顶级集合
keywords:
- 顶级集合 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c433bb6269739dd139ea02e0913f5d767a0bc2c4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820321"
---
# <a name="top-level-collections-opened-by-windows-for-system-use"></a>Windows 打开的供系统使用的顶级集合

Windows 将打开以下 [顶级集合](top-level-collections.md) 以供系统使用：

| 设备类型            | 使用情况页 | 使用 ID | Windows 客户端                                                                                     | 访问模式 |
|------------------------|:----------:|:--------:|----------------------------------------------------------------------------------------------------|-------------|
| 指针                | 0x01       | 0x01     | Win32 子系统                                                                                    | 排他   |
| 鼠标                  | 0x01       | 0x02     | Win32 子系统                                                                                    | 排他   |
| 操纵杆               | 0x01       | 0x04     | DirectInput                                                                                        | 共享      |
| 游戏板               | 0x01       | 0x05     | DirectInput                                                                                        | 共享      |
| Keyboard               | 0x01       | 0x06     | Win32 子系统                                                                                    | 排他   |
| 键盘                 | 0x01       | 0x07     | Win32 子系统                                                                                    | 排他   |
| 系统控制         | 0x01       | 0x80     | Win32 子系统                                                                                    | 共享      |
| 消费者音频控制 | 0x0C       | 0x01     | Windows 2000 和 hidserv.dll (Microsoft Windows XP 中的一个 SVC 主机服务) hidserv.exe | 共享      |
