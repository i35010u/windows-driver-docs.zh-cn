---
title: WIA 平板驱动程序
description: WIA 平板驱动程序
ms.assetid: 83c35b1f-10e0-47e1-97cc-5a7a79fb8088
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d3ba2f9affb0c05218ce660243561248cae846d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533413"
---
# <a name="wia-flatbed-driver"></a>WIA 平板驱动程序





系统提供 WIA 平板驱动程序和供应商提供 microdriver 结合起来以使 WIA 微型驱动程序。 WIA 平板驱动程序从 WIA 服务接收请求，并将请求路由到通过 microdriver 函数 WIA microdriver。 WIA 平板驱动程序将请求发送到 WIA microdriver，后者将发送回 WIA 平板驱动程序的响应。 WIA 平板驱动程序然后将发送到 WIA 服务这些响应。

下面是 WIA 平板驱动程序的功能的说明：

### <a name="minimum-whql-wia-properties"></a>最小 WHQL WIA 属性

WIA 平板驱动程序实现可用属性的一个子集，不允许使用由供应商的任何扩展。 它实现所需的 WHQL 规范这些属性。 请参阅 WHQL 要求规范的详细信息。

### <a name="supported-data-types"></a>支持的数据类型

支持以下数据类型：

-   1 位黑白

-   8 位的灰度

-   24 位颜色

Microdriver 可以排除不支持的设备的数据类型。

### <a name="file-formats"></a>文件格式

默认文件格式是位图 (BMP)。 可以使用添加其他格式的支持[WIA microdriver 可选命令](https://msdn.microsoft.com/library/windows/hardware/ff546016)CMD\_SETFORMAT。

### <a name="supported-transfer-types"></a>受支持的传输类型

支持文件传输和回调传输类型。

### <a name="resolution"></a>分辨率

默认情况下，支持以下解决方法：75、 100、 150，200，300 和 600 dpi。

根据设备的分辨率范围而有所不同，因为可以通过将如下所示的条目添加到将安装程序信息 (INF) 文件来指定可能的解决方法的列表：

```INF
[DeviceData]
Resolutions="75, 100, 300, 600, 1200"
```

**请注意**  请记住每个逗号后面加一个空格。
可以使用**IWiaItem::DeviceDlg**方法 （Microsoft Windows SDK 文档中所述） 来获取用户输入选择"自定义"解决方法。

 

### <a name="adf"></a>ADF

支持只是简单的自动文档送纸器 (ADF) 控制。

 

 




