---
title: 在意外断开连接的情况下结束的 WLAN 会话百分比
description: 该度量来自将 7 天滑动窗口的遥测数据聚合为设备意外断开 Wi-Fi 连接的实例所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7034bdbaa669ba0d4e5de6386a7969f23769559e
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "71017013"
---
# <a name="percent-of-wi-fi-sessions-ending-in-an-unexpected-disconnect"></a>在意外断开连接的情况下结束的 WLAN 会话百分比 

## <a name="description"></a>说明

设备成功连接到 Wi-Fi 后，必须保持该连接，这样设备才能持续访问 Internet。 此度量监视任何意外的 Wi-Fi 断开。 如果用户的设备出现意外的 Wi-Fi 断开连接，则其依赖于 Internet 的应用程序无法正常工作，并在 Internet 访问按钮上显示有警告图标（黄色区域内显示惊叹号），或者计算机完全从 Internet 断开连接。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |7 天|
|度量标准 |实例的聚合|
|最小实例数 |1,000 个实例|
|通过标准 |<= 25% 的实例不以意外的断开连接结束|
|度量 ID |7844359|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为设备意外断开 Wi-Fi 连接的实例所占的百分比  。

   a. 该度量将同一“设备-接入点”对中的多个实例聚合到单个数据点中。

   b. 如果信号强度低于 50%，则该度量不会聚合任何“设备–AP”对。

2. 预期的断开连接为：

   a. 用户断开连接，计算机关机，由于电源状态低而断开连接，或切换到以太网。

3. 意外的断开连接计为“100”，成功的会话计为“0”

### <a name="final-calculation"></a>最终计算

在意外断开连接的情况下结束的 WLAN 会话百分比 = 平均值（所有实例） 
