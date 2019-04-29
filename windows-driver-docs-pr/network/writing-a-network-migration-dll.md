---
title: 编写网络迁移 DLL
description: 编写网络迁移 DLL
ms.assetid: a6a9e57a-cc39-4cdf-a374-4791ddd4a5da
keywords:
- 网络迁移 DLL WDK
- 网络组件升级，WDK，网络迁移 DLL
- 升级网络组件 WDK，DLL 的网络迁移
- 迁移 DLL WDK 网络
- 编写网络迁移 DLL
- Dll WDK 网络迁移
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dab9f0c118ba47e843fbb3f03deac5abe543f1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379785"
---
# <a name="writing-a-network-migration-dll"></a>编写网络迁移 DLL





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

网络迁移 DLL 将从 Microsoft Windows NT 3.51 或 Windows NT 4.0 到 Windows 2000 或更高版本迁移一个或多个网络组件的参数值。

网络迁移 DLL 必须：

-   **加载在升级前操作系统 （Windows NT 3.51 或 Windows 4.0）**

    DLL 不能调用任何函数特定于 Windows 2000 或更高版本，或使用特定于 Windows 2000 或更高版本的任何功能。 如果在 postupgrade （GUI 模式） 阶段中运行该 DLL，必须还将其加载在 Windows 2000 和更高版本操作系统中。

-   **导出** [ **PreUpgradeInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff562439)**并**[**DoPreUpgradeProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff545634)**函数**

    如果在 GUI 模式阶段中运行该 DLL，必须将导出[ **PostUpgradeInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff562410)并[ **DoPostUpgradeProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff545629)函数，为嗯。

-   **Winnt32 阶段做出任何不可逆更改**

    DLL 必须不进行任何不可逆更改，如删除文件或修改注册表项，在此阶段中，因为用户可以取消的网络组件或操作系统升级。 但是，该 DLL 可以修改 NetSetup 对的调用中指定其临时工作目录中的文件**PreUpgradeInitialize**。

 

 





