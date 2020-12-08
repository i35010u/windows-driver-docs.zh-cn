---
title: 附件方案
description: 附件方案
keywords:
- WSDBIT 工具 WDK，测试方案
- WSDAPI 基本互操作性工具 WDK，测试方案
- 方案 WDK WSDBIT
- 测试方案 WDK WSDBIT
- 附件方案 WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95a11cf74100bbceab511aaf3d214e1800024828
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840821"
---
# <a name="attachments-scenarios"></a>附件方案

附件方案测试发送和接收附件。

此方案的目标不是托管服务终结点的发现。 此方案假定在开始此方案之前发现或提供了这些终结点。

在每种情况下，发送到 TestDevice 的附件都将 Dpws1.jpg，并将 Dpws2.jpg 从 TestDevice 收到的附件。 应通过将预期的附件的副本加载到内存中，并对收到的附件执行字节的内存比较来验证附件。

有关详细信息，请参阅 [WSDBIT 测试环境](wsdbit-testing-environment.md)中的初始测试设备安装程序关系图。

|案例|客户端操作|服务器操作|Pass-Fail 条件|
|----|----|----|----|
|**3.1**|**调用单向附件方法**| | |
|3.1.1|调用 AttachmentService 的 **单向** 方法</br>- `wsa:Action == http://schemas.example.org/AttachmentService/OneWayAttachment`</br>- `http:\//testdevice.interop/AttachmentService1` 将使用该服务。</br>-请参阅 [ATTACHMENTSERVICE WSDL](attachmentservice-wsdl.md)。</br>-将 Dpws1.jpg 用作发送到设备的附件的数据。|验证附件数据。|服务器会正确验证附件数据。 服务器接收 Dpws1.jpg。|
|**3.2**|**调用双向附件方法**| | |
|3.2.1|调用 AttachmentService 的 **双向** 方法：</br>- `wsa:Action == http://schemas.example.org/AttachmentService/TwoWayAttachmentRequest`</br>- \/ 将使用 http：/testdevice.interop/AttachmentService1 服务。</br>-请参阅 [ATTACHMENTSERVICE WSDL](attachmentservice-wsdl.md)。</br>-将 Dpws1.jpg 用作发送到设备的附件的数据。|-验证附件数据。</br>-Send **TwoWayAttachmentResponse**。</br>- `wsa:Action == http://schemas.example.org/AttachmentService/TwoWayAttachmentResponse`</br>-请参阅 [ATTACHMENTSERVICE WSDL](attachmentservice-wsdl.md)。</br>-将 Dpws2.jpg 用作返回给客户端的附件的数据。|服务器会正确验证附件数据，客户端会收到响应。 服务器接收 Dpws1.jpg。|
|3.2.2|验证 **TwoWayAttachmentResponse** 中收到的附件数据。 客户端接收 Dpws2.jpg。|无变化。|客户端正确验证附件数据。|
