---
title: 计划购买
description: 计划购买
ms.assetid: e4713e66-a26d-4408-885e-877259e4450b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e964dfae316e81456a73987ce86311e50aa2e81
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563186"
---
# <a name="plan-purchase"></a>计划购买


集成的简单而直观的设备上的计划购买与 Windows 体验可以简化订阅采购流程并允许用户购买订阅时所需的移动连接。

开发计划购买体验涉及以下过程：

-   **确定订阅状态**当启动应用时，它应以智能方式确定设备是否具有当前关联的计划，并且显示了适当经验的基础。 对于现有用户没有当前关联计划，应用可以显示的帐户管理体验和购买订阅的体验。

    若要确定当前的订阅状态，移动宽带应用程序可以获取设备和订阅信息从 Windows — 例如，国际移动 (IMSI)、 集成电路卡 ID (ICCID) 和国际移动设备标识 (IMEI)。 它可以使用移动宽带连接的连接状态来确定用户是否具有一个计划。

-   **购买或次充值体验**（如计划信息、 付款和信用卡验证） 的采购业务逻辑的详细信息必须维护应用程序中。 Windows 支持 web 服务或移动电话网络协议等非结构化补充服务数据 (USSD) 与后端系统，以开发此业务逻辑系统进行交互。

-   **预配**后用户已购买计划，Windows 必须预配设备，你必须激活其后端中的设备。 预配被指配置基于 Windows 的计算机与到运营商网络连接所需的信息。 这通常发生在订阅购买之后。 预配信息包含移动宽带的配置文件 (接入点名称\[APN\]，用户名和密码)，热点的配置文件、 Wi-fi 凭据和计划信息。 Windows 可以使用此信息来自动连接到网络，而无需任何用户输入。 

有关预配的详细信息，请参阅[帐户预配](account-provisioning.md)。

为某些运营商，移动网络上的激活过程不是瞬间完成，可能需要最多十分钟。 您的应用程序必须妥善处理这种情况，并为提供良好的用户体验。 Windows 激活体验应获取估计的激活时间有关的信息，并在购买过程中向用户显示该信息。

设计注意事项包括：

-   **通过检索设备信息来简化用户体验**购买，在您的业务逻辑的要求设备的信息来显示可用于设备的计划。 您的应用程序可以通过使用获取的信息[订阅服务器和设备信息 API](subscriber-and-device-information-api.md); 因此，无需要求用户手动输入此信息。

-   **通过使用预配 API 提供无缝连接体验**用户购买了该计划后，可以将凭据分配给该订阅。 用户必须使用这些凭据和连接参数连接到网络。 可以使用[预配 API](provisioning-api.md)提供此信息。 预配引擎将存储此信息，并自动连接到网络。

-   **选择后端交互**购买计划，用户可以使用有限的连接、 备用 Internet 连接 （主页、 咖啡厅），或者控制通道协议 (USSD)。

以下流程图描述了如何计划购买适用于 Windows 和 UWP 应用：

![计划购买流程图](images/mb-fig1-planpurchaseflowchart.png)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带应用方案](mobile-broadband-app-scenarios.md)

 

 






