---
title: MALT 的微控制器命令
description: 本主题定义了 PC 与微控制器 (Arduino) 的命令，这些命令控制 MALT 中的传感器。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1fe2b9b0e858fec4b64dde52677b5ade79a98a3f
ms.sourcegitcommit: ac28dd2a921c25796d19572a180b88e460420488
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2021
ms.locfileid: "101682208"
---
# <a name="microcontroller-commands-for-malt"></a>MALT 的微控制器命令

本主题定义了 PC 与微控制器 (Arduino) 的命令，这些命令控制 MALT 中的传感器。 建议控制微控制器的计算机也是所测试的系统或设备 (SUT/DUT) 。  

## <a name="serial-command-interface"></a>串行命令接口

通过以下串行命令与测试远程测试机组通信。 每个命令都将在一系列行中写入和读取序列。


### <a name="light-light-level"></a>轻型 *电平*

根据给定输入调整光源级别。

引用中使用的 [光源面板](https://www.superbrightleds.com/moreinfo/led-panel-light/square-12v-led-panel-light-fixture-1ft-x-1ft-35w/2184/) 支持介于 .25 到1.3 伏输入。

对于引用 DAC [微芯片 MCP4821](https://www.microchip.com/wwwproducts/en/MCP4821)使用数据表，可以解决最大 *Vout* 发送到光源面板的情况。

1.3 = 2.048 * 1 * (D/ (2 ^ 12) ) 

D = 2600

**示例：** 

下面的示例将基于) 上方的公式，发送获取最高亮度 (所需的电压。

```cmd
LIGHT 2600
```



**串行输出：**

| 第0行                |
|-----------------------|
| MALTERROR 状态代码 |

### <a name="readalssensor-sensor-number"></a>READALSSENSOR *传感器编号*

传感器编号定义如下：

1. 环境光线传感器 (远离屏幕) 
2. 屏幕光线传感器 (朝向屏幕) 

**示例：**

下面的示例将屏幕光线传感器中生成的原始数据写入串行。 可以基于所使用的传感器的 [数据表](https://www.ti.com/product/OPT3001) 来计算 Lux。

```cmd
READALSSENSOR 2
```

**串行输出：**

| 第0行                  | 第1行                | 第2行                |
|-------------------------|-----------------------|-----------------------|
| 失败时的指数 (0)  | 失败时的结果 (0)  | MALTERROR 状态代码 |

### <a name="readcolorsensor-sensor-number"></a>READCOLORSENSOR *传感器编号*

传感器编号定义如下：

1. 环境颜色传感器 (远离屏幕) 
2. 屏幕颜色传感器 (朝向屏幕) 

**示例：**

下面的示例将屏幕颜色传感器的结果数据写入串行。 这些数字已经历了一个要转换为 XYZ colorspace 的内置校准矩阵。

```cmd
READCOLORSENSOR 2
```

**串行输出：**

| 第1行  | 第2行  | 第3行  |        第4行         |
|---------|---------|---------|-----------------------|
| X 值 | Y 值 | Z 值 | MALTERROR 状态代码 |

### <a name="conversiontime-conversion-time-in-ms"></a>CONVERSIONTIME *转换时间（毫秒*）

引用中使用的 [OPT3001](https://www.ti.com/product/OPT3001) 轻型传感器支持2次转换：800毫秒和100ms。
CONVERSIONTIME 更改两个传感器的转换时间。

> [!NOTE] 
> 如果在写入配置注册时度量转换正在进行，则活动度量转换将立即中止。

**示例：** 

下面的示例将两个传感器的转换时间更改为100ms。

MALT 原型使用的默认转换时间为800毫秒。

```cmd
CONVERSIONTIME 100
```

**串行输出：**

| 第0行                |
|-----------------------|
| MALTERROR 状态代码 |

### <a name="unrecognized-commands"></a>无法识别的命令

对于任何无法识别的命令： 

**串行输出：**

| 第0行                                                                        |
|-------------------------------------------------------------------------------|
| MALTERROR 状态代码 (其中 MALTERROR 状态代码 = `E_UNRECOGNIZED_COMMAND`) |



## <a name="malt-error-code"></a>MALT 错误代码

| E_SUCCESS | E_INVALID_PARAM | E_UNRECOGNIZED_COMMAND |
|-----------| --------------- | ---------------------- |
| 0         | 1               | 2                      |
