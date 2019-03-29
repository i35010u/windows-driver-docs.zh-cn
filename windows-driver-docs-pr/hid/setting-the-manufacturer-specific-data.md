---
title: 设置特定于制造商的数据
description: 设置特定于制造商的数据
ms.assetid: 57787e7a-2a80-476c-8027-b7c154b2f407
keywords:
- INF 文件 WDK 操纵杆制造商特定的数据
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ba6fda05386abdcfb7c4b350ba4287e84b4ced56
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575942"
---
# <a name="setting-the-manufacturer-specific-data"></a>设置特定于制造商的数据





INF 文件所指向特定于制造商的部分包含每个设备都可以安装的一个的项。 每个条目包含安装部分、 设备 ID 和任何兼容的设备的名称后跟的设备的名称。 如果设备已注册为插即用兼容，然后插 ID （从开始有一个星号） 应应用于设备 id。 如果尚未注册设备，则应使用设备 ID 不是插兼容 （即，一个未启动带星号）。 注册时此类设备，请避免选择与其他设备 Id 相冲突的 ID （"游戏杆"例如，不会良好 ID）。

 

 




