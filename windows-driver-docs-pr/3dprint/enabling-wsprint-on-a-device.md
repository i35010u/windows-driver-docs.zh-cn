---
title: 在设备上启用 WSPrint 2.0
description: 使用这些设置在设备上启用 WSPrint 2。0
ms.date: 05/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5d01b0d6fa3a69dffcaf46e50c3263fe8be38657
ms.sourcegitcommit: 32f42241991d57032e5d39ee9f2a3ab4a66ae396
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/18/2020
ms.locfileid: "83553332"
---
# <a name="enable-wsprint-20-on-a-device"></a>在设备上启用 WSPrint 2.0

本主题介绍在设备上启用 WSPrint 2.0 所需的设置。

## <a name="broadcast-a-mdns-printer-service"></a>广播 Mdn 打印机服务

必须使用 PrintService 的服务类型完成此操作。 \_打印机。 \_端口80上的 tcp。

## <a name="implement-a-http-endpoint"></a>实现 HTTP 终结点

终结点需要能够响应 WSPrint 2.0 操作。 不需要执行 SOAP 验证和处理。 您可以改为使用字符串检测和替换。

WSPrint 终结点正常工作后，需要使用自定义设备 id 自定义从 GetPrinterElements 调用返回的 XML：

```xml
<wprt:DeviceId>MFG:MS3D; CMD:XPS; MDL:Compat; CLS:Printer; DES:Compat; CID:MS3DWSD</wprt:DeviceId>
```

此项与已发布 INF 中的兼容 ID 匹配：

```xml
WSDPRINT\MS3DCompatE2D2
```

## <a name="wsprint-interactions"></a>WSPrint 交互

下图显示了 WSPrint 2.0 交互：

![wsprint 交互](images/wsprint-interactions.png)

以下步骤是 WSPrint 2.0 交互的更详细说明：

1. 探测–网络发现启动

2. 解决–网络发现启动

3. 获取–打印机元数据查询

4. GetPrinterElements –打印机元数据查询

5. 订阅–事件模型注册

6. 取消订阅–事件注销

7. SetEventRate –事件速率

8. 续订–续订

9. PrepareToPrint –打印初始化

10. CreatePrintJob –打印提交

11. CreatePrintJob2 –打印提交

12. GetPrintDeviceResources –允许检索 .Resx 中的本地化资源（多部分传出响应）

13. GetPrintDeviceCapabilities-允许检索打印设备功能（多部分传出响应）

14. GetBidiSchemaExtensions-允许检索双向架构扩展（多部分传出响应）

15. CancelJob –作业取消

16. GetActiveJobs –作业进度

17. GetJobHistory –作业历史记录

18. AddDocument –将文档添加到当前打印

19. GetJobElements –获取作业状态

20. SendDocument –实际打印数据（多部分传入请求）

有关 WSPrint 2.0 的详细信息，请参阅以下资源：

[在用于打印的设备上实现 Web 服务](https://docs.microsoft.com/windows-hardware/design/whitepapers/implementing-web-services-on-devices-for-printing)

[WSPrint 2.0 规范](https://docs.microsoft.com/windows-hardware/design/whitepapers/implementing-web-services-on-devices-for-printing#file-downloads)
