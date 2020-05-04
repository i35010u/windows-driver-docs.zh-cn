---
title: 使用元数据配置移动宽带体验的概述
description: 使用元数据配置移动宽带体验的概述
ms.assetid: d3ceab6e-550f-4852-8ee0-4a261c238434
ms.date: 07/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2d6ec527e943738f773826a8a4af4e235a5500fa
ms.sourcegitcommit: 9b791a85c471f0d7707a4a28a2ca273713b7993e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2020
ms.locfileid: "82558848"
---
# <a name="overview-of-using-metadata-to-configure-mobile-broadband-experiences"></a>使用元数据配置移动宽带体验的概述

> [!IMPORTANT] 
> 从 Windows 10 版本1703开始，APN 数据库被称为 COSA 的新格式所取代。 1703之前的 windows 10 windows 8、Windows 8.1 和版本将继续使用 APN 数据库，Windows 10 版本1703和更高版本使用 COSA。 有关 COSA 的详细信息，请参阅[COSA 概述](cosa-overview.md)。
>
> 从 Windows 10 版本1803开始，MBAE 应用体验被 "UWP 应用" 的 MO 概述取代。 有关 UWP 应用的 MO 概述的详细信息，请参阅[uwp mobile 宽带应用概述](uwp-mobile-broadband-apps.md)。

可提供元数据来自定义 Windows 8、Windows 8.1 和 Windows 10 移动版宽带应用程序的各个方面。 其中包括自定义带有操作员品牌的 Windows 连接管理器、将移动宽带应用与 Windows 连接管理器集成、为 Windows APN 数据库提供更新的信息以及提供用于预配 PC 的数据。 Windows 8、Windows 8.1 和 Windows 10 包含可使用的元数据的三个源：

-   **WINDOWS APN 数据库**Windows APN 数据库包含首次连接到操作员网络所需的预设置的数据。 该数据库是 Windows 8、Windows 8.1 和 Windows 10 的一部分，并且通过使用 Windows update 概述进行更新。 Windows APN 数据库在电脑上始终可用。 有关 COSA 和 APN 数据库的详细信息，请参阅[COSA/APN 数据库](cosa-apn-database.md)。

-   **服务元数据**订阅购买和操作员品牌所需的信息。 提供此信息是服务元数据包的一部分。 它存储在 Windows 元数据和 Internet 服务（WMIS）中，并在使用任何可用的 Internet 连接检测到移动宽带设备后下载。 此元数据还可以由 OEM 预装到电脑上，但你必须预安装从 Windows 开发人员中心-硬件的 "硬件开发人员" 部分下载的包。 有关服务元数据的详细信息，请参阅[服务元数据](service-metadata.md)。

-   **帐户预配元数据**购买订阅后生成的信息，包括 Wi-fi 凭据和计划信息。 此元数据由你在付款验证后由你提供给 Windows，并可通过使用预配-刷新机制进行更新。 有关帐户预配元数据的详细信息，请参阅[帐户预配](account-provisioning.md)。

下图显示了不同的元数据源如何相关以及如何为它们提供服务。 服务元数据优先于 Windows APN 数据库中的信息。

![这是移动宽带的概述](images/mbae-sxs-overview.jpg)

使用此部分中的链接了解有关不同类型移动宽带元数据的详细信息概述：

-   [帐户预配](account-provisioning.md)

-   [COSA/APN 数据库](cosa-apn-database.md)

-   [服务元数据](service-metadata.md)
