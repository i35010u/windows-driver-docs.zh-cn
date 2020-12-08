---
title: 访问和修改文件
description: 访问和修改文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74f7d78be451763e3ba099429a78fb1756bb4078
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826283"
---
# <a name="accessing-and-modifying-files"></a>访问和修改文件


以下准则适用于在访问或修改文件时使用的驱动程序包组件：

-   只能在 INF 文件中使用 [inf 指令](./inf-addcomponent-directive.md) 来修改文件。 例如，使用 INF [**CopyFiles**](inf-copyfiles-directive.md) 指令复制文件，使用 inf [**RenFiles**](inf-renfiles-directive.md) 指令来重命名文件。

-   Inf [**CopyFiles**](inf-copyfiles-directive.md) 指令中显示的文件不能同时出现在 inf [**RenFiles**](inf-renfiles-directive.md) 或 Inf 文件中的 [**DelFiles**](inf-delfiles-directive.md) 指令中。

**重要提示**  必须谨慎使用 INF [**RenFiles**](inf-renfiles-directive.md) 和 [**DelFiles**](inf-delfiles-directive.md) 指令。 不应在 INF 文件中使用这些指令来 (PnP) 函数驱动程序的即插即用。

 

 

