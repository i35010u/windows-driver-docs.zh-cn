---
title: 使用仪表板 API 报告硬件故障
description: 这些异步方法用于访问 Win10/Win8.x 驱动程序错误和 OEM 硬件错误的报告数据。
ms.topic: article
ms.localizationpriority: medium
ms.date: 04/05/2018
ms.openlocfilehash: 28bb769ea30b7a8f14e0f68a506f128671d21b24
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "63335040"
---
# <a name="hardware-failure-reporting"></a>硬件故障报告

使用这些异步方法可以访问 Windows 8 和 Windows 10 驱动程序和 OEM 硬件错误的报告数据。 

可根据需要定义报告模板、设置计划，系统会定期向你传送数据。 

## <a name="prerequisites"></a>必备条件 

若要使用此方法，首先需要执行以下操作： 
* 如果尚未开始操作，请先完成 Microsoft Store 分析 API 的所有 [先决条件](https://docs.microsoft.com/windows/uwp/monetize/access-analytics-data-using-windows-store-services) 。 

* 获取 [Azure AD 访问令牌](https://docs.microsoft.com/windows/uwp/monetize/access-analytics-data-using-windows-store-services) ，以供在此方法的请求标头中使用。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。 

有关详细信息，请参阅“使用 Microsoft Store 服务访问分析数据”  

> [!IMPORTANT]
> 提醒一下，[Windows Analytics 协议](https://go.microsoft.com/fwlink/?linkid=866941)声明：“你的个人信息存储时间不得超过三十 (30) 天。 在这 30 天期限过后，你将立即销毁个人信息。” 

