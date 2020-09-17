---
title: 删除设备的注册表项
description: 删除设备的注册表项
ms.assetid: BA7AB3B4-9751-4e53-98AD-2B920F7223A1
keywords:
- 注册表 WDK 设备安装，删除设备的注册表项
- 删除注册表项 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5aeca4e1c15e92aa239d451a70f269f8a9693ff1
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717126"
---
# <a name="deleting-the-registry-keys-of-a-device"></a>删除设备的注册表项


由于以下原因，不应使用设备的 **SetupDiDeleteDevRegKey** 或 *硬件密钥* ：

-   [**SetupDiDeleteDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdideletedevregkey) 删除注册表项中的所有自定义设置。 这包括：

    -   在安装过程中指定的设置。

    -   设备驱动程序创建或修改的设置。

    -   由应用程序或其他组件创建或修改的设置。

    [**SetupDiDeleteDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdideletedevregkey) 还会删除关键设备安装状态。

-   使用 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey) 打开的软件或硬件密钥与 DICS_FLAG_GLOBAL 范围包含有关设备安装状态的数据。 使用范围 DICS_FLAG_CONFIGSPECIFIC 访问的软件或硬件密钥不包含设备安装状态。

    在这两种情况下，删除这些软件或硬件密钥可能会影响其他设备安装组件。

不应假设设备注册表项是否存在。 卸载设备后，系统会自动删除设备的所有软件和硬件密钥。

可以通过使用标准注册表功能，安全地创建和删除硬件或软件密钥下的注册表子项。 通过使用这些函数，可避免系统和其他组件之间的命名冲突。 此外，如果使用这些函数创建子项，子项将继承父注册表项的默认权限。 有关详细信息，请参阅 [打开、创建和关闭密钥](https://go.microsoft.com/fwlink/p/?linkid=194541)。

有关标准注册表函数的详细信息，请参阅 [注册表函数](https://go.microsoft.com/fwlink/p/?linkid=194529)。

 

