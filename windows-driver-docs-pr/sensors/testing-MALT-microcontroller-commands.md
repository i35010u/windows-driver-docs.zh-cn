---
title: MALT 的微型控制器命令
author: windows-driver-content
description: 本主题定义在电脑和微型控制器 (Arduino) 控制在 MALT 传感器之间的命令。
ms.assetid: 38b9c6fc-f13c-4af5-90ab-d9931dc9b7f1
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: b6e73d78f584724d27ed882cccfa632501fdf2c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362223"
---
# <a name="microcontroller-commands-for-malt"></a>MALT 的微型控制器命令

本主题定义在电脑和微型控制器 (Arduino) 控制在 MALT 传感器之间的命令。 我们建议，控制微控制器的 PC 也是系统或待测试 (SUT/DUT) 的设备。  

## <a name="serial-command-interface"></a>串行命令界面

与以下串行命令通过远程测试机组进行通信。 每个命令将写入和读取从串行对一系列行。


### <a name="light-light-level"></a>光*浅色级别*

调整光级别基于给定的输入。

[浅面板](https://www.superbrightleds.com/moreinfo/led-panel-light/square-12v-led-panel-light-fixture-1ft-x-1ft-35w/2184/).25 和 1.3 之间支持的引用中使用伏的输入。

使用数据工作表引用 DAC[微芯片 MCP4821](https://www.microchip.com/wwwproducts/en/MCP4821)，我们可解决的最大值*Vout*将发送到浅色面板。

1.3 = 2.048 * 1 * (D/(2^12))

D = 2600

**示例：** 

以下示例发送来使光线的最大亮度 （基于上述公式中） 所需的电压。

```cmd
LIGHT 2600
```



**串行输出：**

| 行 0                |
|-----------------------|
| MALTERROR 状态代码 |

### <a name="readalssensor-sensor-number"></a>READALSSENSOR*传感器数*

传感器号定义，如下所示：

1. 环境光线传感器 （背屏幕）
2. 屏幕光线传感器 （面向向屏幕）

**示例：**

下面的示例将从屏幕光线传感器生成的原始数据写入到串行。 可以根据计算 lux[数据表](https://www.ti.com/product/OPT3001)的传感器使用。

```cmd
READALSSENSOR 2
```

**串行输出：**

| 行 0                | 第 1 行                  | 第 2 行                |
|-----------------------|-------------------------|-----------------------|
| MALTERROR 状态代码 | 指数 (0 失败) | 结果 (0 失败) |

### <a name="readcolorsensor-sensor-number"></a>READCOLORSENSOR*传感器数*

传感器号定义，如下所示：

1. 环境颜色传感器 （背屏幕）
2. 屏幕颜色传感器 （面向向屏幕）

**示例：**

下面的示例将从屏幕颜色传感器生成的原始数据写入到串行。 可以根据计算 lux[数据表](https://www.ti.com/product/OPT3001)的传感器使用。

```cmd
READCOLORSENSOR 2
```

**串行输出：**

| 行 0                | 第 1 行    | 第 2 行      | 第 3 行     |
|-----------------------|-----------|-------------|------------|
| MALTERROR 状态代码 | 红色值 | 绿色值 | 蓝色的值 |

### <a name="conversiontime-conversion-time-in-ms"></a>CONVERSIONTIME*以毫秒为单位的转换时间*

[OPT3001](https://www.ti.com/product/OPT3001)在引用中使用的光线传感器支持 2 个转换时间：800 毫秒和 100 毫秒。
CONVERSIONTIME 更改这两个传感器的转换时间。

> [!NOTE] 
> 如果度量转换过程中写入配置注册时，活动测量转换将立即中止。

**示例：** 

下面的示例更改为 100 毫秒的两个传感器的转换时间。

使用 MALT 原型的默认转换时间是 800 毫秒。

```cmd
CONVERSIONTIME 100
```

**串行输出：**

| 行 0                |
|-----------------------|
| MALTERROR 状态代码 |

### <a name="unrecognized-commands"></a>无法识别的命令

对于任何无法识别的命令： 

**串行输出：**

| 行 0                |
|-----------------------|
| MALTERROR 状态代码 |

其中 MALTERROR 状态代码 = `E_UNRECOGNIZED_COMMAND`

## <a name="malt-error-code"></a>MALT 错误代码

| E_SUCCESS | E_INVALID_PARAM | E_UNRECOGNIZED_COMMAND |
|-----------| --------------- | ---------------------- |
| 0         | 1               | 2                      |