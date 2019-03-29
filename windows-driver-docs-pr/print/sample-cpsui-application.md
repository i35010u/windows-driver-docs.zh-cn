---
title: 示例 CPSUI 应用程序
description: 示例 CPSUI 应用程序
ms.assetid: 895afbfe-c18a-4bcc-b815-8cb323bbac80
keywords:
- 常用属性页用户界面 WDK 打印，示例
- CPSUI WDK 打印，示例
- 属性表页 WDK 打印示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8947ca126ea84b915b41e064e75239b6f8a40ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564020"
---
# <a name="sample-cpsui-application"></a>示例 CPSUI 应用程序





中包含的源代码 CPSUISAM，示例 CPSUI 应用程序， \\src\\WDK 的打印目录。 应用程序会导致 CPSUI 以调入打印后台处理程序创建属性表页的系统的默认打印机。 然后，应用程序创建其他属性表页，以演示一些可以使用 CPSUI 创建一个新页面时所采用的技术。

**请注意**  打印机接口 Dll 不应调用到打印后台处理程序。 CPSUISAM 演示了其中一些 CPSUI 的功能，但不表示应由打印机接口的 Dll 的技术。 相反，这些 Dll 应遵循的步骤中所述[与打印机驱动程序使用 CPSUI](using-cpsui-with-printer-drivers.md)。

 

 

 




