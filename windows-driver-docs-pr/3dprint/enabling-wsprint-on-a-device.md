---
title: 在设备上启用 WSPrint 2.0
description: 使用这些设置在设备上启用 WSPrint 2.0
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5942989ce749569d87966d3ea403aab5cca803c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325461"
---
# <a name="enable-wsprint-20-on-a-device"></a>在设备上启用 WSPrint 2.0


本主题介绍在设备上启用 WSPrint 2.0 所需的设置。

## <a name="broadcast-a-mdns-printer-service"></a>广播 Mdn 打印机服务


此操作必须执行使用 PrintService 的服务类型。\_打印机。\_tcp.local 端口 80 上的。

## <a name="implement-a-http-endpoint"></a>实现 HTTP 终结点 


终结点必须是能够响应 WSPrint 2.0 操作。 不需要执行 SOAP 验证和处理。 您可以使用字符串检测和替换。

一旦 WSPrint 终结点正常工作，需要自定义从自定义设备 id GetPrinterElements 调用返回的 XML:

```xml
<wprt:DeviceId>MFG:MS3D; CMD:XPS; MDL:Compat; CLS:Printer; DES:Compat; CID:MS3DWSD</wprt:DeviceId>
```
这与已发布的 INF 中的兼容 ID 相匹配：

```xml
WSDPRINT\MS3DCompatE2D2
```

## <a name="wsprint-interactions"></a>WSPrint 交互


下图显示了 WSPrint 2.0 交互：

![wsprint 交互](images/wsprint-interactions.png)

以下步骤是 WSPrint 2.0 交互的更详细的说明：

1.  探测 – 启动网络发现

2.  解决 – 启动网络发现

3.  Get – 打印机元数据查询

4.  GetPrinterElements – 打印机元数据查询

5.  订阅 – 事件模型注册

6.  取消订阅 – 事件取消注册

7.  SetEventRate – 事件速率

8.  续订-续订 

9.  PrepareToPrint – 打印初始化

10. CreatePrintJob – 打印提交

11. CreatePrintJob2 – 打印提交

12. GetPrintDeviceResources – 允许检索的 ResX （多部分传出响应） 中的本地化资源

13. GetPrintDeviceCapabilities-允许检索的打印设备功能 （多部分传出响应）

14. GetBidiSchemaExtensions-允许检索 Bidi 架构扩展 （多部分传出响应）

15. CancelJob – 作业取消

16. GetActiveJobs – Job Progress 

17. GetJobHistory – 作业历史记录

18. AddDocument – 添加到当前打印的文档

19. GetJobElements-获取作业状态

20. SendDocument – 实际打印数据 （多部分传入的请求）

WSPrint 2.0 的详细信息，请参阅以下资源：

[在用于打印的设备上实现 Web 服务](https://go.microsoft.com/fwlink/p/?linkid=867155)

[WSPrint 2.0 规范](https://go.microsoft.com/fwlink/p/?LinkId=534008) 



