---
title: 选择源文件
description: 选择源文件
ms.assetid: 259a7092-1197-4521-853a-6064aaa0c037
keywords:
- INF 文件 WDK 游戏杆，源文件
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6b50448289795d5be097fda85eefd76212b2eea1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519937"
---
# <a name="selecting-source-files"></a>选择源文件





INF 文件的"SourceDisksFiles"部分指定要复制哪些文件。 这包括所有必需的驱动程序，以及任何其他文件，如文档和设置应用程序。 这可能是要在用户的系统上安装的第一个游戏杆驱动程序，如系统游戏杆驱动程序 Vjoyd.vxd 和 Msjstrick.drv 应复制，除了此设备的特定驱动程序。 应建立通过对 Layout.inf （导致用户提示输入 Windows 95/98/我安装光盘） 的引用并不分布在 OEM 光盘上的以下两个驱动程序源。驱动程序应复制到用户的系统目录中，这是目标代码 11。

 

 




