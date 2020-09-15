---
title: 访问和修改文件
description: 访问和修改文件
ms.assetid: DD5A527F-5F8D-4892-A2D5-C0279913B6A3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ee4e7a5544199c30dc0dd683f295eaf10eac482
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104198"
---
# <a name="accessing-and-modifying-files"></a>访问和修改文件


以下准则适用于在访问或修改文件时使用的驱动程序包组件：

-   只能在 INF 文件中使用 [inf 指令](./inf-addcomponent-directive.md) 来修改文件。 例如，使用 INF [**CopyFiles**](inf-copyfiles-directive.md) 指令复制文件，使用 inf [**RenFiles**](inf-renfiles-directive.md) 指令来重命名文件。

-   Inf [**CopyFiles**](inf-copyfiles-directive.md) 指令中显示的文件不能同时出现在 inf [**RenFiles**](inf-renfiles-directive.md) 或 Inf 文件中的 [**DelFiles**](inf-delfiles-directive.md) 指令中。

**重要提示**   必须谨慎使用 INF [**RenFiles**](inf-renfiles-directive.md)和[**DelFiles**](inf-delfiles-directive.md)指令。 不应在 INF 文件中使用这些指令来 (PnP) 函数驱动程序的即插即用。

 

 

