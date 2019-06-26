---
title: UMDF 驱动程序的初级指南
description: UMDF 驱动程序的初级指南
ms.assetid: 67EF6762-AA31-4D35-8EB3-04F9CD34C7D1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3da3014f3ae3c8ea6e8c7cb59fec3b9db80c31af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376179"
---
# <a name="session-zero-guidelines-for-umdf-drivers"></a>UMDF 驱动程序的初级指南


从 Windows Vista 中，操作系统将隔离服务和运行后续会话 0，而应用程序中的系统进程、 更高版本带编号的会话。 由于 UMDF 主机进程 (WUDFHost.exe) 是一个在会话 0 中运行的系统进程，UMDF 驱动程序是独立于应用程序。 因此，开发您的驱动程序时必须使用以下准则：

-   不要创建一个用户界面 (UI) 元素，如对话框中，或依赖于用户输入。 用户未在会话 0 中运行，因为他或她永远不会看到用户界面，不能对其做出响应。

    同样，不操作任何 UI 元素。 例如，UMDF 驱动程序不能在用户的会话中枚举 windows。

-   如果您的驱动程序必须与服务通信，使用远程过程调用 (RPC) 或命名的管道等的客户端/服务器机制。
-   在 Windows API 中调用函数时要格外小心。 某些函数可能操作的 UI 元素，或尝试访问用户的会话中的命名的对象。 请勿调用不会调用从用户模式服务的 Windows 函数。 作为一般规则，kernel32.dll，在导出的函数，但不是在 user32.dll 导出的函数，可以安全地调用 UMDF 驱动程序。

    UMDF 驱动程序可能会调用 Windows 函数来执行以下任务：

    -   驱动程序可能会在调用 **SetupDi * * * Xxx*函数来检索插设备属性。 例如， [UMDF 示例驱动程序用于 OSR USB Fx2 学习工具包](https://go.microsoft.com/fwlink/p/?linkid=256202)调用[ **SetupDiGetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)检索设备的总线类型的 GUID。
        **请注意**  UMDF 驱动程序不能安全地调用许多 **SetupDi * * * Xxx*函数，但它是安全地调用检索设备节点属性的函数。

         

    -   从手动队列中检索输入/输出请求的驱动程序可能会创建定期计时器轮询队列。 例如， [WudfVhidmini](https://go.microsoft.com/fwlink/p/?linkid=256226)示例将通过调用注册计时器回调例程[ **CreateThreadpoolTimer**](https://docs.microsoft.com/windows/desktop/api/threadpoolapiset/nf-threadpoolapiset-createthreadpooltimer)，然后通过调用设置定期计时器[ **SetThreadpoolTimer**](https://docs.microsoft.com/windows/desktop/api/threadpoolapiset/nf-threadpoolapiset-setthreadpooltimer)。
        **请注意**  1.11 版中，从开始，UMDF 工作项中提供支持。 有关详细信息，请参阅[使用工作项](using-workitems.md)。

         

有关使用外部框架的系统服务的其他信息，请参阅 14 章 （"超出框架"） 的 Orwick，尾和专家 Smith。 *使用 Windows Driver Foundation 开发驱动程序*。 Redmond，WA:Microsoft Press，2007年。

有关会话 0 隔离的其他信息，请参阅[服务和 Windows 中的驱动程序的影响的会话 0 隔离](https://go.microsoft.com/fwlink/p/?linkid=240132)。

 

 





