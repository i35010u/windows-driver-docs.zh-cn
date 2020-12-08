---
title: 源代码窗格中的文件
description: 源代码窗格中的文件
keywords:
- 静态驱动程序验证器报表 WDK，源代码窗格
- 源代码窗格 WDK 静态驱动程序验证程序
- 文件 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6eebebe897975fca02fcdbe158418760ad041363
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804249"
---
# <a name="files-in-the-source-code-pane"></a>源代码窗格中的文件


仅当文件所包含的代码引起或检测规则冲突时，文件才会出现在 " **源代码** " 窗格中。 因此，对于同一驱动程序的不同规则冲突，窗口中将显示不同的文件。

以下类型的文件显示在 "源代码" 窗格中：

<span id="Driver_source_files"></span><span id="driver_source_files"></span><span id="DRIVER_SOURCE_FILES"></span>**驱动程序源文件**  
该驱动程序的源文件以及它所使用的库的源文件，这涉及到规则冲突。 这组文件包括 C 文件和头文件。

<span id="rule_source_file___________________.slic__"></span><span id="RULE_SOURCE_FILE___________________.SLIC__"></span>**规则源文件 (\\** _ _ *. slic* *  **)**  
验证中 [静态驱动程序验证程序规则](static-driver-verifier-rule.md) 的源文件。 此代码以规范语言编写，用于 (SLIC) ，这是为此目的而开发的一种简单语言。

<span id="sdv-harness.c_"></span><span id="SDV-HARNESS.C_"></span>**sdv**   
验证中规则的 SDV [操作系统模型](operating-system-model.md) 的源文件。

 

 





