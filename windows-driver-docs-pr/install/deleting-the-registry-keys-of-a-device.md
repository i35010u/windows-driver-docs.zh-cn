---
title: 删除设备的注册表项
description: 删除设备的注册表项
ms.assetid: BA7AB3B4-9751-4e53-98AD-2B920F7223A1
keywords:
- 删除设备的注册表项的注册表 WDK 设备安装
- 正在删除注册表项 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ef9e28fc56f907915eb6f88b8bebf6057b7bbb6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521105"
---
# <a name="deleting-the-registry-keys-of-a-device"></a>删除设备的注册表项


不应使用**SetupDiDeleteDevRegKey**或*硬件密钥*出于以下原因设备：

-   [**SetupDiDeleteDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff550991)删除注册表项中的所有自定义设置。 这包括以下内容：

    -   在安装过程中指定的设置。

    -   已创建或修改的设备驱动程序的设置。

    -   已创建或修改的应用程序或其他组件的设置。

    [**SetupDiDeleteDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff550991)还会删除重要的设备安装状态。

-   使用打开的软件或硬件密钥[ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079)与 DICS_FLAG_GLOBAL 的作用域包含有关设备安装状态的数据。 软件或硬件与 DICS_FLAG_CONFIGSPECIFIC 的作用域访问的项不包含设备安装状态。

    在任一情况下，删除这些软件或硬件密钥可能会影响其他设备安装组件。

不应造成会假设设备注册表项是否存在。 卸载设备后，系统将自动删除该设备的所有软件和硬件密钥。

可以安全地创建以及使用标准注册表函数删除硬件或软件项下的注册表子项。 通过使用这些函数，可以避免命名系统和其他组件之间的冲突。 此外，如果使用这些函数创建子项，子项将继承父注册表项的默认权限。 有关详细信息，请参阅[打开、 创建、 和关闭密钥](https://go.microsoft.com/fwlink/p/?linkid=194541)。

有关标准注册表函数的详细信息，请参阅[注册表函数](https://go.microsoft.com/fwlink/p/?linkid=194529)。

 

 





