---
title: WIA 平板驱动程序
description: WIA 平板驱动程序
ms.assetid: 83c35b1f-10e0-47e1-97cc-5a7a79fb8088
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b24a4d2b76bf75891d9cb6a8d45d5538b74c47d2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191499"
---
# <a name="wia-flatbed-driver"></a>WIA 平板驱动程序





系统提供的 WIA 平板驱动程序和供应商提供的 microdriver 组合为 WIA 微型驱动程序。 WIA 平板驱动程序接收来自 WIA 服务的请求，并通过 microdriver 函数将请求路由到 WIA microdriver。 WIA 平板驱动程序将请求发送到 WIA microdriver，后者将响应发送回 WIA 平板驱动程序。 然后，WIA 平台驱动程序将这些响应发送到 WIA 服务。

下面是 WIA 平板驱动程序功能的说明：

### <a name="minimum-whql-wia-properties"></a>最小 WHQL WIA 属性

WIA 平板驱动程序仅实现了一部分可用属性，不允许供应商进行任何扩展。 它仅实现 WHQL 规范所需的那些属性。 有关详细信息，请参阅 WHQL 要求规范。

### <a name="supported-data-types"></a>支持的数据类型

支持以下数据类型：

-   1位黑色/白色

-   8位灰度

-   24位颜色

Microdriver 可以排除设备不支持的数据类型。

### <a name="file-formats"></a>文件格式

默认的文件格式是 (BMP) 的位图。 其他格式支持可以使用 [WIA microdriver 可选命令](./optional-commands.md) CMD \_ SETFORMAT 添加。

### <a name="supported-transfer-types"></a>支持的传输类型

文件传输类型和回叫传输类型都受支持。

### <a name="resolution"></a>解决方法

默认情况下，支持以下解决方案：75、100、150、200、300和 600 dpi。

由于解决方案范围因设备而异，因此可以通过将以下条目（如下所示）添加到安装信息 (INF) 文件中来指定可能的解析列表：

```INF
[DeviceData]
Resolutions="75, 100, 300, 600, 1200"
```

**注意**   请记得在每个逗号后面加一个空格。
在选择 "自定义" 解决方法时，可以使用 Microsoft Windows SDK 文档) 中介绍的 **IWiaItem：:D evicedlg** 方法 (来获取用户输入。

 

### <a name="adf"></a>ADF

仅支持简单的自动文档送纸器 (ADF) 控制。

 

