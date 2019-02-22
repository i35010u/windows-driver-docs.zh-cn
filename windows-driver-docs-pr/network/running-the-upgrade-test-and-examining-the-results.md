---
title: 运行升级测试并检查结果
description: 运行升级测试并检查结果
ms.assetid: 82a2427e-94ed-4f7e-93e7-7952ca0d98e8
keywords:
- 测试网络组件升级 WDK
- 升级测试 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 629d08fe474c3aaa181b437a3abfb555c91d8d3d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544995"
---
# <a name="running-the-upgrade-test-and-examining-the-results"></a>运行升级测试并检查结果





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

在升级到 Windows 2000 或更高版本的系统之前，请注意每个要升级的网络组件的注册表中的参数值。

**若要运行升级测试**

1.  请确保包含已检验的版本的 Windows 2000 或更高版本在 CD-ROM CD-ROM 驱动器。

2.  在测试系统上运行 winnt32.exe。 例如，使用以下命令以 cd-rom 放入驱动器 o： 的基于 Intel 的系统上运行 winnt32.exe
    ```CMD
    winnt32.exe /s:o\i386
    ```

3.  安装 Windows 2000 或更高版本后，验证已升级的网络组件的参数已正确迁移到新的操作系统。

 

 





