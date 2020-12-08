---
title: GPD 架构的新关键字
description: GPD 架构的新关键字
keywords:
- 根级别关键字 WDK 打印机自动配置
- GPD 文件 WDK GDL 扩展，关键字
- 关键字 WDK 打印机自动配置
- 内置自动配置支持 WDK 打印机，关键字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8ae01874a9772c6763339ac4f13910b311c7914
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807807"
---
# <a name="new-keyword-for-gpd-schema"></a>GPD 架构的新关键字


从 Windows Vista 开始，你应该向 GPD 文件中添加一个新的根级别关键字，该关键字指向 GPD，BidiQueryFile 中的 GDL 文件 \* **BidiQueryFile**，它将标识一个 GDL 文件，其中包含自动配置所需的双向映射信息。 如果缺少关键字，则自动配置不需要调用 GDL 分析器或再次点击文件系统来搜索 GDL 文件。

如果要编写基于 Unidrv 的驱动程序，则必须使用 GDL 文件，驱动程序的主 GPD 文件通过使用 BidiQueryFile 关键字直接引用该文件 \* *_BidiQueryFile_* 。

 

 




