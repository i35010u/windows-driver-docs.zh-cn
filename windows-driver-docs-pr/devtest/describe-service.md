---
title: 在移动宽带元数据创作向导中描述服务
description: 在移动宽带元数据创作向导中描述服务
ms.assetid: 0FA4945C-3CD9-4106-BC47-F89CEF168FDC
keywords:
- 在移动宽带元数据创作向导中描述服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8eba754f1d11af03ab5d5605fd16304906b8dfb4
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769621"
---
# <a name="describe-your-service-in-the-mobile-broadband-metadata-authoring-wizard"></a>在移动宽带元数据创作向导中描述服务

你可以在 Windows 中提供有关你的服务的描述性信息，如型号名称和制造商。

### <a name="to-provide-descriptive-information-about-a-service"></a>提供有关服务的描述性信息

1. 单击 "**说明**" 选项卡。
2. 填写以下字段。
    - **服务名称**。 此可选字段未在 Windows 8 中使用。
    - **服务提供商**。 出现在 Windows 连接管理器中的运算符名称。
    - **服务号**。 指定唯一标识服务的 GUID。 使用 operator XML 预配时，此 GUID 用于标识运算符。 如果更新设备元数据包，则此 GUID 应保持不变。
        **注意** 此值与设备元数据包的体验 ID 和文件名不同。 有关为服务编号选择 GUID 的详细信息，请参阅[使用元数据配置移动宽带体验概述](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/using-metadata-to-configure-mobile-broadband-experiences)。

- **说明 1**。 此可选字段未在 Windows 8 中使用。
- **描述 2**。 此可选字段未在 Windows 8 中使用。

有关元数据属性的详细信息，请参阅[服务元数据包架构参考](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/service-metadata-package-schema-reference)。
