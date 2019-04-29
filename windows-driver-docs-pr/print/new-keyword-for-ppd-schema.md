---
title: PPD 架构的新关键字
description: PPD 架构的新关键字
ms.assetid: 05caa402-4949-4c0f-913c-1c87e65c30d7
keywords:
- 根级别的关键字 WDK 打印机自动配置
- PPD 文件 WDK 自动配置关键字
- 关键字 WDK 打印机自动配置
- 框中自动配置支持 WDK 打印机，关键字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aca48475ae56745bb52cd7decd34bfecc9b64b7c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355902"
---
# <a name="ew-keyword-for-ppd-schema"></a>PPD 架构的新关键字


到 PPD 文件指向中 PPD GDL 文件应为 Windows Vista 和更高版本的 Windows 中，添加一个新的根级别关键字\* **MSBidiQueryFile**，这将标识包含 bidi GDL 文件映射所需的自动配置的信息。 如果缺少关键字，则自动配置不需要调用 GDL 分析器或达到文件系统中再次以搜索 GDL 文件。

开发人员编写基于 PScript 的驱动程序必须使用单独 GDL 文件的驱动程序的主 PPD 文件引用直接使用\* **MSBidiQueryFile**关键字。

 

 




