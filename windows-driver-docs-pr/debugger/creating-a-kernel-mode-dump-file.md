---
title: 创建内核模式转储文件
description: 创建内核模式转储文件
ms.assetid: d3eb86b2-eba7-4ddb-90e9-0e26414436fb
keywords:
- 转储文件，创建内核模式转储文件
- 转储文件、 NMI 开关
- NMI 开关
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9198aa1b0d552078bc9058d402d5911073a9aa3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374455"
---
# <a name="creating-a-kernel-mode-dump-file"></a>创建内核模式转储文件


## <span id="ddk_creating_a_kernel_mode_dump_file_dbg"></span><span id="DDK_CREATING_A_KERNEL_MODE_DUMP_FILE_DBG"></span>


有三种方法可以在其中创建内核模式转储文件：

1.  您可以启用控制面板中的转储文件，然后系统可能会崩溃本身。

2.  您可以启用控制面板中的转储文件，然后强制系统崩溃。

3.  可以使用调试器不导致系统崩溃的情况下创建一个转储文件。

本部分包括：

[启用内核模式转储文件](enabling-a-kernel-mode-dump-file.md)

[强制在系统发生崩溃](forcing-a-system-crash.md)

[正在创建而无需在系统发生崩溃转储文件](creating-a-dump-file-without-a-system-crash.md)

[验证创建内核模式转储文件](verifying-the-creation-of-a-kernel-mode-dump-file.md)

### <a name="span-idusingannmiswitchspanspan-idusingannmiswitchspanusing-an-nmi-switch"></a><span id="using_an_nmi_switch"></span><span id="USING_AN_NMI_SWITCH"></span>使用 NMI 开关

还有可能要 NMI 开关用于创建崩溃转储文件。 请联系硬件供应商，以确定你的计算机是否具有此开关。

此文档中未涵盖 NMI 开关的使用情况。

 

 





