---
title: 将 GDL 扩展添加到现有的 PPD 文件
description: 将 GDL 扩展添加到现有的 PPD 文件
ms.assetid: 4d425701-85af-43e8-9ff2-ddfcc755f90c
keywords:
- 框中自动配置支持 WDK 打印机，GDL 扩展
- GDL 文件 WDK 打印机
- 扩展 WDK GDL 文件
- PPD 文件 WDK 自动配置，GDL 扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 737178efe7180ccfc87f59c5b1280b97c0e633c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354109"
---
# <a name="adding-gdl-extensions-to-an-existing-ppd-file"></a>将 GDL 扩展添加到现有的 PPD 文件


如果你想要将自动配置的支持添加到现有的现成 PPD 文件，请按照下列步骤：

1.  创建 GDL 文件。 GDL 文件应具有\* **BidiQuery**并\* **BidiResponse**对应的元素\***功能**/\***选项**PPD 文件中指定构造。 请注意，必须执行此操作仅对需要 bidi 信息的功能。

2.  包括 GDL 文件依赖于驱动程序的文件列表的一部分。

本部分包括：

[新关键字 PPD 架构](new-keyword-for-ppd-schema.md)

[自动配置 PPD 的 Windows Vista 中的流](autoconfig-flow-in-windows-vista-for-ppd.md)

[添加构造 PPD GDL 文件](adding-constructs-to-your-gdl-file-for-ppd.md)

 

 




