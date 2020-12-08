---
title: UMDF 驱动程序的初级指南
description: UMDF 驱动程序的初级指南
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 785636177194774236ac07fa74fd8dae60e2f78a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821147"
---
# <a name="session-zero-guidelines-for-umdf-drivers"></a>UMDF 驱动程序的初级指南


从 Windows Vista 开始，操作系统将隔离会话0中的服务和系统进程，而应用程序会在后续的编号较高的会话中运行。 因为 UMDF 主机进程 ( # A0) 是在会话0中运行的系统进程之一，所以，UMDF 驱动程序与应用程序隔离。 因此，在开发驱动程序时，必须使用以下准则：

-   请勿 (UI) 元素创建用户界面，如对话框，或依赖于用户输入。 由于用户未在会话0中运行，因此，他或她永远看不到该 UI，无法响应。

    同样，不要操作任何 UI 元素。 例如，UMDF 驱动程序无法枚举用户会话中的 windows。

-   如果你的驱动程序必须与服务进行通信，请使用客户端/服务器机制（如远程过程调用 (RPC) 或命名管道）。
-   在 Windows API 中调用函数时请小心。 某些函数可能会处理 UI 元素或尝试访问用户会话中的命名对象。 不要调用不会从用户模式服务调用的 Windows 函数。 作为一般规则，UMDF 驱动程序可以安全地调用 kernel32.dll 中导出的函数，但不能调用 user32.dll 中导出的函数。

    UMDF 驱动程序可以调用 Windows 函数来执行以下任务：

    -   驱动程序可以调用 **SetupDi**_Xxx_ 函数来检索即插即用设备属性。 例如， [OSR USB Fx2 学习工具包的 UMDF 示例驱动程序](/samples/browse/) 调用 [**SetupDiGetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya) 来检索设备总线类型的 GUID。
        **注意**  UMDF 驱动程序无法安全地调用许多 **SetupDi**_Xxx_ 函数，但调用检索设备节点属性的函数是安全的。

         

    -   从手动队列检索 i/o 请求的驱动程序可能会创建一个周期性计时器以轮询队列。 例如， [WudfVhidmini](/samples/browse/) 示例通过调用 [**CreateThreadpoolTimer**](/windows/win32/api/threadpoolapiset/nf-threadpoolapiset-createthreadpooltimer)来注册计时器回调例程，然后通过调用 [**SetThreadpoolTimer**](/windows/win32/api/threadpoolapiset/nf-threadpoolapiset-setthreadpooltimer)来设置一个周期性计时器。
        **注意**  从版本1.11 开始，UMDF 提供对工作项的支持。 有关详细信息，请参阅 [使用工作项](using-workitems.md)。

         

有关在框架外使用系统服务的其他信息，请参阅 Orwick、、Smith 和人员 Smith ) 的 "框架" 之外的第14个 (。 *开发包含 Windows Driver Foundation 的驱动程序*。 华盛顿州雷蒙德市：微软出版社，2007。

有关会话零隔离的其他信息，请参阅在 [Windows 中对服务和驱动程序进行会话0隔离的影响](/previous-versions/windows/hardware/design/dn653293(v=vs.85))。

