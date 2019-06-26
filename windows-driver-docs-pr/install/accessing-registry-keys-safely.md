---
title: 安全地访问注册表项
description: 安全地访问注册表项
ms.assetid: 81203790-66CB-42ee-82F8-2F0FFF04DF10
keywords:
- 注册表 WDK 设备安装，安全地访问注册表项
- 访问注册表密钥安全地 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c096e156a2432fb372de612248605991926047d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386050"
---
# <a name="accessing-registry-keys-safely"></a>安全地访问注册表项


客户问题频繁跟踪到了过外部组件，如第三方[设备安装应用程序](writing-a-device-installation-application.md)，执行以下操作：

-   删除关键注册表项。

-   修改关键注册表项的访问权限。

很多与外部组件出现的问题而引起的注册表项使用 KEY_ALL_ACCESS 访问权限。 从 Windows Server 2003 [ **SetupDiCreateDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)授予访问权限和不 KEY_ALL_ACCESS 唯一 KEY_READ 和 KEY_WRITE。 从 Windows Vista 开始，都会强制执行其他 KEY_ALL_ACCESS 限制。

请遵循以下准则可以安全地访问注册表项：

-   使用 SetupAPI 并*软件密钥*设备。

    这些函数解决常见的问题而导致的访问权限的限制。

-   Windows 不同版本之间可能会更改的位置和注册表项的格式。 不要假设位置、 格式或含义的注册表项或值用于设备和驱动程序安装。

    有关注册表项和树的详细信息，请参阅[注册表树和设备和驱动程序的密钥](registry-trees-and-keys.md)。

-   不要使用注册表来直接访问或修改设备的内部设置。

-   请求所需的每个任务，如下所示的最小访问权限：

    -   KEY_SET_VALUE

    -   KEY_CREATE_SUB_KEY

    -   KEY_QUERY_VALUE

    -   KEY_ENUMERATE_SUB_KEYS

-   不要直接打开设备安装程序类项在注册表中。 与任何注册表项，可能会更改的 Windows 不同版本之间的位置和设备安装程序类项的名称。

    若要安全地打开设备安装程序类密钥，请遵循以下准则：

    -   使用[ **SetupDiOpenClassRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey)。

    -   使用[ **SetupDiOpenClassRegKeyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)并设置 DIOCR_INSTALLER*标志*参数。

-   不要直接打开设备接口的类密钥在注册表中。 与任何注册表项，可能会更改的 Windows 不同版本之间的位置和设备接口的类密钥的名称。

    若要安全地打开设备接口的类密钥，请使用[ **SetupDiOpenClassRegKeyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)并设置 DIOCR_INSTALLER*标志*参数。

-   使用仅 INF 指令来修改由操作系统使用的保留的注册表项。 有关详细信息，请参阅[INF 指令摘要](summary-of-inf-directives.md)。

-   *类安装程序*并*共同安装程序*不能调用注册表函数来创建、 更改或删除由操作系统保留供使用的注册表值。

    有关详细信息，请参阅[访问共同安装程序类安装程序进行注册表](accessing-the-registry-by-class-installers-and-co-installers.md)。

有关注册表项的访问权限的详细信息，请参阅[注册表项安全和访问权限](https://go.microsoft.com/fwlink/p/?linkid=194542)。

 

 





