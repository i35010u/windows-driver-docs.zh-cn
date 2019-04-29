---
title: 源代码窗格中的文件
description: 源代码窗格中的文件
ms.assetid: 1bc248be-cdc8-4e6c-9eca-da2943daaf58
keywords:
- 静态驱动程序验证工具报表 WDK，源代码窗格
- 源代码窗格 WDK Static Driver Verifier
- 文件 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81f18aed8e785ac522b5c42e8d2f1148f4e8fa55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378817"
---
# <a name="files-in-the-source-code-pane"></a>源代码窗格中的文件


文件显示在**源代码**窗格仅时导致或检测的规则冲突中涉及它们所包含的代码。 因此，不同的文件在不同的规则冲突的窗口中显示相同的驱动程序。

源代码窗格中显示以下类型的文件：

<span id="Driver_source_files"></span><span id="driver_source_files"></span><span id="DRIVER_SOURCE_FILES"></span>**驱动程序源文件**  
该驱动程序，以及它使用的规则冲突中涉及的库的源代码文件。 此文件组包括 C 文件和头文件。

<span id="rule_source_file___________________.slic__"></span><span id="RULE_SOURCE_FILE___________________.SLIC__"></span>**规则源文件 (\\*** **.slic** **)**  
为源文件[Static Driver Verifier 规则](static-driver-verifier-rule.md)中验证。 此代码是用规范语言编写的接口检查 （slic 表），一种简单的语言开发实现此目的。

<span id="sdv-harness.c_"></span><span id="SDV-HARNESS.C_"></span>**sdv-harness.c**   
SDV 源文件[操作系统模型](operating-system-model.md)中验证规则。

 

 





