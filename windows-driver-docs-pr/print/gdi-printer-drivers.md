---
title: GDI 打印机驱动程序
description: GDI 打印机驱动程序
ms.assetid: c7ae6c0e-ae43-4b10-9a6f-f2daf578ecd2
keywords:
- GDI 打印机驱动程序 WDK
- 打印机驱动程序 WDK GDI
- GDI 打印机驱动程序 WDK，有关 GDI 打印机驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 384f47b4ae2950af2dd74d377bffed3301de4443
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575924"
---
# <a name="gdi-printer-drivers"></a>GDI 打印机驱动程序





所有 Windows 2000 和更高版本的打印机驱动程序都包括以下组件：

-   一个[打印机图形 DLL](printer-graphics-dll.md) ，可帮助 GDI 呈现打印作业，并将呈现的数据的流发送到打印后台处理程序。

-   一个[打印机接口 DLL](printer-interface-dll.md)提供驱动程序的配置参数，这两个的用户界面和后台处理程序的接口可以调用以通知与打印相关的系统事件的驱动程序。

此外，Microsoft 提供的打印机驱动程序请利用[打印机数据文件](printer-data-files.md)。

 

 




