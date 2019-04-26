---
title: 常见数据字段
description: 本主题说明在所有特定于传感器的数据字段中包含的常见数据字段。
ms.assetid: 5F9F7987-E898-404A-96F9-F5CF88F01393
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 956333d250f31653da9f9c263fc5abfe5dec5a49
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325266"
---
# <a name="common-data-fields"></a>常见数据字段


本主题说明在所有特定于传感器的数据字段中包含的常见数据字段。

客户端可以使用 ReadFile 函数以检索这些数据字段信息。

下表显示了常见的数据字段。

有关类型列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|描述|
| --- | --- | --- | --- |
|PKEY_SensorData_Timestamp|VT_FILETIME|必需|文件时间计算 UTC 格式中的驱动程序。 类扩展 (CX) 提供了一个 helper 函数来将计时周期数从启动转换为 FILETIME，以便远程系统不需要的系统时钟同步。|

 

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






