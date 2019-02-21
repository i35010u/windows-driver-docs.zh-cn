---
title: 路径信息的模式信息的关系
description: 路径信息的模式信息的关系
ms.assetid: 214717dd-1c01-4daf-9296-586299668d3a
keywords:
- 连接显示 WDK Windows 7 的显示器、 CCD 概念、 模式和路径信息
- 连接显示 WDK Windows Server 2008 R2 显示、 CCD 概念、 模式和路径的信息
- 配置显示 WDK Windows 7 的显示器、 CCD 概念、 模式和路径信息
- 配置显示 WDK Windows Server 2008 R2 显示、 CCD 概念、 模式和路径的信息
- CCD 概念 WDK Windows 7 显示、 模式和路径信息
- CCD 概念 WDK Windows Server 2008 R2 显示、 模式和路径信息
- 模式和路径信息 WDK Windows 7 显示
- 模式和路径信息 WDK Windows Server 2008 R2 显示
- WDK Windows 7 显示的路径和模式信息
- WDK Windows Server 2008 R2 显示的路径和模式信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53658021a130763c19ac750fa3a2c73acecafa1e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546372"
---
# <a name="relationship-of-mode-information-to-path-information"></a>路径信息的模式信息的关系


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215) CCD 函数始终返回路径信息和特定显示配置的源和目标模式信息。 下图显示了示例的源和目标模式信息与路径信息的方式。 在此示例中，QDC\_所有\_路径标志传递给*标志*对的调用中的参数**QueryDisplayConfig**。

![说明的路径信息的模式信息的关系的关系图](images/displayconfigpathandmode.png)

 

 





