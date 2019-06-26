---
title: 打印机 INF 文件的 CopyFiles 节
description: 打印机 INF 文件的 CopyFiles 节
ms.assetid: 92c96019-d2dd-4b2c-818a-80ae091ec662
keywords:
- INF 文件 WDK 打印，CopyFiles 部分
- 部分 WDK 打印机
- CopyFiles 指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d97d30dedc040951457687ea49408cd22730ba94
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356058"
---
# <a name="printer-inf-file-copyfiles-sections"></a>打印机 INF 文件的 CopyFiles 节





当打印机 INF 文件包含引用的文件列表部分[ **INF CopyFiles 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)，必须使用以下格式指定的文件列表中每个文件：

**\[** <em>file-list-section</em> **\]** 
*destination-file-name\[,,flag\]* 
*destination-file-name\[,,flag\]* 
*destination-file-name\[,,flag\]* ...*目标文件名*字段是必需的并且*标志*字段是可选的。 文件规范不能包含可选*源文件名*或*临时文件名*文件定义的字段的列表与 INF CopyFiles 指令一起使用的部分。 此限制是在网页上安装打印驱动程序所必需的。

 

 




