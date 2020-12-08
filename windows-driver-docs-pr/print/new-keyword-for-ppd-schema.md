---
title: 用于 PPD 架构的 new 关键字
description: 用于 PPD 架构的 new 关键字
keywords:
- 根级别关键字 WDK 打印机自动配置
- PPD 文件 WDK 自动配置，关键字
- 关键字 WDK 打印机自动配置
- 内置自动配置支持 WDK 打印机，关键字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1aafcbbd0e97f255389fbc2d3216d46996fbd77
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807803"
---
# <a name="ew-keyword-for-ppd-schema"></a>用于 PPD 架构的 new 关键字


对于 Windows Vista 和更高版本的 Windows，应将新的根级别关键字添加到 PPD 文件中，该文件指向 PPD，MSBidiQueryFile 中的 GDL 文件 \* **MSBidiQueryFile**，该文件会标识 GDL 文件，其中包含了自动配置所需的双向映射信息。 如果缺少关键字，则自动配置不需要调用 GDL 分析器或再次点击文件系统来搜索 GDL 文件。

编写基于 PScript 的驱动程序的开发人员必须使用单独的 GDL 文件，驱动程序的主要 PPD 文件直接使用 \* *_MSBidiQueryFile_* 关键字进行引用。

 

 




