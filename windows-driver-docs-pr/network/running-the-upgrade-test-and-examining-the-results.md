---
title: 运行升级测试并检查结果
description: 运行升级测试并检查结果
keywords:
- 测试网络组件升级 WDK
- 升级测试 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 900e7f39d11d94cac206022091f9c894b3f12d6b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815893"
---
# <a name="running-the-upgrade-test-and-examining-the-results"></a>运行升级测试并检查结果





**注意**  Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

将系统升级到 Windows 2000 或更高版本之前，请注意注册表中要升级的每个网络组件的参数值。

**运行升级测试**

1.  请确保 cd-rom 驱动器中包含 Windows 2000 或更高版本的已选中版本。

2.  在测试系统上运行 winnt32.exe。 例如，使用下面的命令，在使用驱动器 O：的 cd-rom 上运行 winnt32.exe：
    ```CMD
    winnt32.exe /s:o\i386
    ```

3.  安装 Windows 2000 或更高版本后，请验证已升级的网络组件的参数是否已正确迁移到新的操作系统。

 

 





