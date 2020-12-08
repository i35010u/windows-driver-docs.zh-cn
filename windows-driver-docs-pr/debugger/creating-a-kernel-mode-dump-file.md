---
title: 创建内核模式转储文件
description: 创建内核模式转储文件
keywords:
- 转储文件，创建内核模式转储文件
- 转储文件，NMI 交换机
- NMI 交换机
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 818269a824098a336d5d9a5dce363faaa9fc31c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836877"
---
# <a name="creating-a-kernel-mode-dump-file"></a>创建内核模式转储文件


## <span id="ddk_creating_a_kernel_mode_dump_file_dbg"></span><span id="DDK_CREATING_A_KERNEL_MODE_DUMP_FILE_DBG"></span>


可以通过三种方式创建内核模式转储文件：

1.  你可以从 "控制面板" 中启用转储文件，然后系统可能会崩溃。

2.  你可以从 "控制面板" 中启用转储文件，然后强制系统崩溃。

3.  您可以使用调试器来创建转储文件，而不会使系统崩溃。

本节包括：

[启用内核模式转储文件](enabling-a-kernel-mode-dump-file.md)

[强制系统崩溃](forcing-a-system-crash.md)

[未发生系统崩溃的情况下创建转储文件](creating-a-dump-file-without-a-system-crash.md)

[验证是否已创建内核模式转储文件](verifying-the-creation-of-a-kernel-mode-dump-file.md)

### <a name="span-idusing_an_nmi_switchspanspan-idusing_an_nmi_switchspanusing-an-nmi-switch"></a><span id="using_an_nmi_switch"></span><span id="USING_AN_NMI_SWITCH"></span>使用 NMI 交换机

还可以使用 NMI 交换机来创建故障转储文件。 请与您的硬件供应商联系，以确定您的计算机是否具有此开关。

此文档不包含 NMI 交换机的使用情况。

 

 





