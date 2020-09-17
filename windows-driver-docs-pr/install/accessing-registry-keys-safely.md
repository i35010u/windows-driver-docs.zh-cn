---
title: 安全地访问注册表项
description: 安全地访问注册表项
ms.assetid: 81203790-66CB-42ee-82F8-2F0FFF04DF10
keywords:
- 注册表 WDK 设备安装，安全访问注册表项
- 在安全的 WDK 设备安装中访问注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22cce21e78a0746b282c1fb8e9f5659e4eda6f35
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717154"
---
# <a name="accessing-registry-keys-safely"></a>安全地访问注册表项


客户问题经常被跟踪到外部组件（例如第三方 [设备安装应用程序](writing-a-device-installation-application.md)），这些组件执行以下操作：

-   删除关键的注册表项。

-   修改关键注册表项的访问权限。

外部组件出现的许多问题都是通过对注册表项的 KEY_ALL_ACCESS 访问权限而引起的。 从 Windows Server 2003 开始， [**SetupDiCreateDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdicreatedevregkeya) 仅授予 KEY_READ 和 KEY_WRITE 访问权限，而不 KEY_ALL_ACCESS。 从 Windows Vista 开始，将强制实施其他 KEY_ALL_ACCESS 限制。

遵循以下准则以安全访问注册表项：

-   对设备使用 Setupapi.log 和 *software 密钥* 。

    这些函数解决了对访问权限的限制导致的常见问题。

-   不同版本的 Windows 之间的注册表项的位置和格式可能会发生变化。 不要假设用于设备和驱动程序安装的注册表项或值的位置、格式或含义。

    有关注册表项和树的详细信息，请参阅 [设备和驱动程序的注册表树和密钥](registry-trees-and-keys.md)。

-   不要使用注册表直接访问或修改设备的内部设置。

-   仅请求每个任务所需的最小访问权限，如下所示：

    -   KEY_SET_VALUE

    -   KEY_CREATE_SUB_KEY

    -   KEY_QUERY_VALUE

    -   KEY_ENUMERATE_SUB_KEYS

-   不要直接在注册表中打开设备安装程序类键。 与任何注册表项一样，设备安装程序类键的位置和名称在不同版本的 Windows 中可能会发生变化。

    若要安全地打开设备安装程序类密钥，请遵循以下准则：

    -   请使用 [**SetupDiOpenClassRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkey)。

    -   使用 [**SetupDiOpenClassRegKeyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa) 并在 *Flags* 参数中设置 DIOCR_INSTALLER。

-   不要直接打开注册表中的设备接口类键。 与任何注册表项一样，设备接口类键的位置和名称在不同版本的 Windows 中可能会发生变化。

    若要安全地打开设备接口类密钥，请使用 [**SetupDiOpenClassRegKeyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa) 并在 *Flags* 参数中设置 DIOCR_INSTALLER。

-   仅使用 INF 指令来修改保留供操作系统使用的注册表项。 有关详细信息，请参阅 [INF 指令摘要](summary-of-inf-directives.md)。

-   *类安装* 程序和 *共同安装程序* 不能调用注册表功能来创建、更改或删除保留供操作系统使用的注册表值。

有关注册表项的访问权限的详细信息，请参阅 [注册表项安全性和访问权限](https://go.microsoft.com/fwlink/p/?linkid=194542)。

 

