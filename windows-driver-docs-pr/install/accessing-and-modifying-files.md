---
title: 访问和修改文件
description: 访问和修改文件
ms.assetid: DD5A527F-5F8D-4892-A2D5-C0279913B6A3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41f18a1da45c2fe994992ac92768ef14435123de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375727"
---
# <a name="accessing-and-modifying-files"></a>访问和修改文件


访问或修改文件时，以下准则适用于驱动程序程序包组件：

-   应仅通过使用修改的文件[INF 指令](inf-directives.md)INF 文件中。 例如，使用 INF [ **CopyFiles** ](inf-copyfiles-directive.md)指令以复制文件和 INF [ **RenFiles** ](inf-renfiles-directive.md)指令以重命名文件。

-   显示在 INF 文件[ **CopyFiles** ](inf-copyfiles-directive.md)指令还不能出现在 INF [ **RenFiles** ](inf-renfiles-directive.md)或[ **DelFiles** ](inf-delfiles-directive.md)指令 INF 文件中。

**重要**  INF [ **RenFiles** ](inf-renfiles-directive.md)并[ **DelFiles** ](inf-delfiles-directive.md)指令必须谨慎使用。 您不应使用 INF 文件中的这些指令 (PnP) Plug and play 功能驱动程序。

 

 

 





