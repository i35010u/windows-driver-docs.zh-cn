---
title: 计划购买
description: 计划购买
ms.assetid: e4713e66-a26d-4408-885e-877259e4450b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0caaf8fa19fead7ff5a85d857273dfe2f212903d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209841"
---
# <a name="plan-purchase"></a>计划购买


与 Windows 体验集成的简单且直观的设备上计划购买可简化订阅获取过程，并让用户在需要移动连接时购买订阅。

开发计划购买体验涉及以下内容：

-   **确定订阅状态** 当应用程序启动时，它应智能地确定设备是否有当前关联的计划，并根据该计划显示适当的体验。 对于没有当前关联计划的现有用户，应用可以显示帐户管理体验和购买订阅体验。

    若要确定当前的订阅状态，移动宽带应用可以从 Windows 获取设备和订阅信息，例如，国际移动用户身份 (IMSI) 、集成的卡 ID (ICCID) 和国际移动设备标识 (IMEI) 。 它可以使用 mobile 宽带连接的连接状态来确定用户是否具有计划。

-   **购买或顶级体验** 必须在你的应用中维护 (的采购业务逻辑详细信息，如计划信息、支付和信用卡验证) 。 Windows 支持 web 服务或移动电话协议，如非结构化补充服务数据 (USSD) ，以便与后端系统进行交互以开发此业务逻辑。

-   **预配** 在用户购买计划后，Windows 必须预配设备，并且必须在其后端激活设备。 预配定义为：将基于 Windows 的计算机配置为连接到运营商网络所需的信息。 这通常发生在购买订阅之后。 设置信息包含移动宽带配置文件 (访问点名称 \[ APN \] 、用户名和密码) 、热点配置文件、wi-fi 凭据和计划信息。 Windows 可以使用此信息自动连接到网络，无需用户输入。 

有关预配的详细信息，请参阅 [帐户预配](account-provisioning.md)。

对于某些运营商，移动网络上的激活过程不是即时的，可能需要长达十分钟的时间。 你的应用程序必须处理此案例完美地，并为用户带来良好的体验。 Windows 激活体验应该获取有关预计激活时间的信息，并在购买过程中向用户显示该信息。

设计注意事项包括：

-   **通过检索设备信息来简化用户体验** 在购买过程中，业务逻辑需要设备信息来显示适用于设备的计划。 应用可以使用 [订阅者和设备信息 API](subscriber-and-device-information-api.md)获取信息;因此，您无需要求用户手动输入此信息。

-   **使用预配 API 提供无缝连接体验** 用户购买计划后，你可以将凭据分配给订阅。 用户必须使用这些凭据和连接参数连接到你的网络。 你可以使用 [预配 API](provisioning-api.md) 来提供此信息。 预配引擎将存储此信息并自动连接到网络。

-   **选择后端交互** 对于购买计划，用户可以使用受限连接、备用 Internet 连接 (home、咖啡店) 或控制通道协议 (USSD) 。

以下流程图介绍了如何使用 Windows 和 UWP 应用进行计划购买：

![规划购买流程图](images/mb-fig1-planpurchaseflowchart.png)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带应用方案](./account-management.md)

 

