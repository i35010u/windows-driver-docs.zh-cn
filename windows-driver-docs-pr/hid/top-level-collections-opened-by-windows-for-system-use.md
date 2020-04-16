---
title: Windows 打开的供系统使用的顶级集合
description: Windows 打开的供系统使用的顶级集合
ms.assetid: e489ce46-379e-4ba9-a0e3-5848b1f4a17b
keywords:
- 顶级集合 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 310793a6853c78fd7382274cb7353d697d9c4dd4
ms.sourcegitcommit: f8c3585ec7b1bdfcd65f7f2cc9aa688655de4d20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81396311"
---
# <a name="top-level-collections-opened-by-windows-for-system-use"></a>Windows 打开的供系统使用的顶级集合

Windows 将打开以下[顶级集合](top-level-collections.md)以供系统使用：

| 设备类型            | 使用情况页 | 使用 ID | Windows 客户端                                                                                     | 访问模式 |
|------------------------|:----------:|:--------:|----------------------------------------------------------------------------------------------------|-------------|
| 指针                | 0x01       | 0x01     | Win32 子系统                                                                                    | 排他   |
| 鼠标                  | 0x01       | 0x02     | Win32 子系统                                                                                    | 排他   |
| 操纵杆               | 0x01       | 0x04     | DirectInput                                                                                        | Shared      |
| 游戏板               | 0x01       | 0x05     | DirectInput                                                                                        | Shared      |
| 键盘               | 0x01       | 0x06     | Win32 子系统                                                                                    | 排他   |
| 键盘                 | 0x01       | 0x07     | Win32 子系统                                                                                    | 排他   |
| 系统控制         | 0x01       | 0x80     | Win32 子系统                                                                                    | Shared      |
| 消费者音频控制 | 0x0C       | 0x01     | Windows 2000 中的 hidserv 和 hidserv （其中一个 SVC 主机服务）在 Microsoft Windows XP 中 | Shared      |
