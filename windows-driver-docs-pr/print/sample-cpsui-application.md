---
title: 示例 CPSUI 应用程序
description: 示例 CPSUI 应用程序
keywords:
- 公共属性表用户界面 WDK 打印，示例
- CPSUI WDK 打印，示例
- 属性表页 WDK 打印，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03a1da9da7df3f224bce787e74d7f4a48138c9ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806997"
---
# <a name="sample-cpsui-application"></a>示例 CPSUI 应用程序





\\WDK 的 src 打印目录中包含 CPSUISAM （示例 CPSUI 应用程序）的源代码 \\ 。 应用程序会导致 CPSUI 调入打印后台处理程序，以便为系统的默认打印机创建属性表页。 然后，该应用程序会创建一个附加的属性表页，以说明在使用 CPSUI 创建新页时可以使用的一些技术。

**注意**  打印机接口 Dll 不应调入打印后台处理程序。 CPSUISAM 阐释了 CPSUI 的一些功能，但并不代表打印机接口 Dll 应使用的技术。 相反，这些 Dll 应遵循在 [打印机驱动程序中使用 CPSUI](using-cpsui-with-printer-drivers.md)中所述的步骤。

 

 

 




