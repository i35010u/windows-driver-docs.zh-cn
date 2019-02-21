---
title: 附件方案
description: 附件方案
ms.assetid: bd563919-961f-40eb-ad5c-26026fc1c0e6
keywords:
- WSDBIT 工具 WDK，测试方案
- WSDAPI 基本互操作性工具 WDK，测试方案
- 方案 WDK WSDBIT
- 测试方案 WDK WSDBIT
- 附件方案 WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5875e0ad98b27392f1bc8ab8d55a57d02d1b458c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519572"
---
# <a name="attachments-scenarios"></a>附件方案


附件方案测试发送和接收附件。

此方案的目标不是承载的服务终结点的发现。 此方案假定这些终结点已发现或在此方案开始之前提供。

在所有情况下，发送到 TestDevice 附件将 Dpws1.jpg 并且 TestDevice 从收到的附件将 Dpws2.jpg。 应通过加载到内存中预期的附件的副本并执行操作上收到的附件的字节的字节的内存比较验证附件。

有关详细信息，请参阅中的初始测试设备安装程序关系图[WSDBIT 测试环境](wsdbit-testing-environment.md)。

本例中客户端操作服务器操作启用通过/失败条件**3.1**

**调用 OneWay 附件方法**

3.1.1

调用**OneWay**与 AttachmentService 方法

-   **wsa:Action = = http://schemas.example.org/AttachmentService/OneWayAttachment**

-   http://testdevice.interop/AttachmentService1将使用服务。

-   请参阅[AttachmentService WSDL](attachmentservice-wsdl.md)。

-   使用 Dpws1.jpg 作为数据发送到设备的附件。

验证附件数据。

在服务器正确验证附件的数据。 服务器接收 Dpws1.jpg。

**3.2**

**调用 TwoWay 附件方法**

3.2.1

调用**TwoWay**与 AttachmentService 方法：

-   **wsa:Action = = http://schemas.example.org/AttachmentService/TwoWayAttachmentRequest**

-   http://testdevice.interop/AttachmentService1将使用服务。

-   请参阅[AttachmentService WSDL](attachmentservice-wsdl.md)。

-   使用 Dpws1.jpg 作为附件发送到设备的数据。

<!-- -->

-   验证附件数据。

-   发送**TwoWayAttachmentResponse**。

-   **wsa:Action = = http://schemas.example.org/AttachmentService/TwoWayAttachmentResponse**

-   请参阅[AttachmentService WSDL](attachmentservice-wsdl.md)。

-   使用 Dpws2.jpg 作为数据返回到客户端的附件。

服务器正确验证附件数据和客户端接收的响应。 服务器接收 Dpws1.jpg。

3.2.2

验证中收到的附件数据**TwoWayAttachmentResponse**。 客户端收到 Dpws2.jpg。

无。

客户端正确验证附件的数据。

 

 

 





