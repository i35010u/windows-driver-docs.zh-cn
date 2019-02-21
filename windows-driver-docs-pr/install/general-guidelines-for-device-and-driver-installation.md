---
title: 设备和驱动程序安装的通用指南
description: 设备和驱动程序安装的通用指南
ms.assetid: E62906AB-CE32-4b07-B7DB-F523FFE4E6C2
keywords:
- 设备安装 WDK，一般指导原则
- 驱动程序安装 WDK，一般指导原则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0932ff8a78ebeac39edfc7bac798efe4807114c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541090"
---
# <a name="general-guidelines-for-device-and-driver-installation"></a>设备和驱动程序安装的通用指南


设备和驱动程序安装在 Windows 操作系统上的基本目标是使过程尽可能轻松为用户。 安装过程和组件的你[驱动程序包](driver-packages.md)应与操作系统的无缝协作[设备安装组件](https://msdn.microsoft.com/library/windows/hardware/ff541277)。

若要提供最佳用户体验，请使用以下指导原则来设计和实现您的安装过程：

-   不会自动重新启动系统或要求用户在执行此操作，除非绝对必要。

-   始终使用[INF 文件](inf-files.md)设备安装的。 请确保所有的 INF 文件格式正确，并使用正确的语法。

-   安装; 完成后将保留在系统上的 INF 文件不要删除这些文件。 不仅设备或驱动程序是首次安装时，而且还在一个驱动程序的用户请求更新通过设备管理器中，使用 INF 文件。

-   使用之一[系统定义设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff553419)。 除非有充足的理由这样做，则未定义您自己的安装程序类。

-   不要假设位置、 格式或注册表项或值的含义。 有关注册表项和树的详细信息，请参阅[注册表树和设备和驱动程序的密钥](registry-trees-and-keys.md)。

 

 





