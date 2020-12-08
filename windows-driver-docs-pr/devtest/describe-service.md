---
title: 在移动宽带元数据创作向导中描述服务
description: 在移动宽带元数据创作向导中描述服务
keywords:
- 在移动宽带元数据创作向导中描述服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cdf40f5907c138d56c5450f8286be09db6ec2a3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839761"
---
# <a name="describe-your-service-in-the-mobile-broadband-metadata-authoring-wizard"></a>在移动宽带元数据创作向导中描述服务

你可以在 Windows 中提供有关你的服务的描述性信息，如型号名称和制造商。

### <a name="to-provide-descriptive-information-about-a-service"></a>提供有关服务的描述性信息

1. 单击 " **说明** " 选项卡。
2. 填写以下字段。
    - **服务名称**。 此可选字段未在 Windows 8 中使用。
    - **服务提供商**。 出现在 Windows 连接管理器中的运算符名称。
    - **服务号**。 指定唯一标识服务的 GUID。 使用 operator XML 预配时，此 GUID 用于标识运算符。 如果更新设备元数据包，则此 GUID 应保持不变。
        **注意**  此值与设备元数据包的体验 ID 和文件名不同。 有关为服务编号选择 GUID 的详细信息，请参阅 [使用元数据配置移动宽带体验概述](../mobilebroadband/using-metadata-to-configure-mobile-broadband-experiences.md)。

- **说明 1**。 此可选字段未在 Windows 8 中使用。
- **描述 2**。 此可选字段未在 Windows 8 中使用。

有关元数据属性的详细信息，请参阅 [服务元数据包架构参考](../mobilebroadband/mobilebroadbandinfo-xml-schema.md)。
