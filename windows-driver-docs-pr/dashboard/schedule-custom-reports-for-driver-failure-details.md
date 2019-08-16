---
title: 计划自定义报告来提供驱动程序失败详细信息
description: 用于针对 Microsoft 硬件开发人员中心创建和计划错误报告的流程概述。
ms.topic: article
ms.author: shganesh
ms.date: 09/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 975be663e70872404d842e0729775f316679b609
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364435"
---
# <a name="schedule-custom-reports-for-your-driver-failure-details"></a>计划自定义报告来提供驱动程序失败详细信息

可以使用这些异步方法访问 Win10/Win8.x 驱动程序错误和 OEM 硬件错误的报告数据。 你可以根据需要定义报告模板、设置计划，系统将会定期向你提供数据。

>[!NOTE]
>
> - 这些方法仅可供属于 [Windows 硬件开发人员中心计划](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-started-with-the-hardware-dashboard)的开发人员帐户使用。
> - 可以使用这些方法替代现有方法来确定 [Windows 10 驱动程序错误](https://docs.microsoft.com/windows/uwp/monetize/get-error-reporting-data-for-windows-10-drivers)、[Windows 7 和 Windows 8.x 驱动程序错误](https://docs.microsoft.com/windows/uwp/monetize/get-error-reporting-data-for-windows-7-and-windows-8.x-drivers)（对于 IHV）和[硬件错误](https://docs.microsoft.com/windows/uwp/monetize/get-oem-hardware-error-reporting-data)（对于 OEM）。
> - 这些方法公开了一组丰富的新维度，并支持回顾过去 90 天的数据。
> - [Swagger](https://apidocs.microsoft.com/services/analyticsreportingapis) 中也提供了 API 文档

## <a name="prerequisites"></a>必备条件

> [!IMPORTANT]
> 必须完成[启用安全数据共享](enable-secure-data-sharing.md)中概述的要求。

若要使用此方法，首先需要执行以下操作：

- 如果尚未完成“Microsoft Store 分析 API”的所有[先决条件](https://docs.microsoft.com/windows-hardware/drivers/dashboard/dashboard-api#complete-prerequisites-for-using-the-microsoft-hardware-api)，请完成这些先决条件，包括获取要在此方法的请求标头中使用的 Azure AD 访问令牌。 请注意，获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。

有关详细信息，请参阅[使用 Microsoft Store 服务访问分析数据](https://docs.microsoft.com/windows/uwp/monetize/access-analytics-data-using-windows-store-services)

> [!IMPORTANT]
> 提醒一下，[Windows Analytics 协议](https://go.microsoft.com/fwlink/?linkid=866941)声明：“你的个人信息存储时间不得超过三十 (30) 天。 在这 30 天期限过后，你将立即销毁个人信息。”

## <a name="workflow-to-schedule-custom-reports-for-driver-failure"></a>用于计划驱动程序失败自定义报告的工作流

下图解释了用于创建新的报告模板，计划自定义报告并检索失败数据的 API 调用模式。

![图中从上到下显示了从创建自定义报告模板，计划自定义报告模板，获取报告数据到 cab 下载之间的工作流。](./images/async-api-flow.png)

1. 客户端应用程序以 JSON 格式定义报告架构，并调用[创建报告模板 API](create-a-new-report-template.md)。

2. 成功时，“新建报告模板 API”将返回 TemplateId。

3. 客户端应用程序使用 TemplateId 以及报告开始日期、重复间隔和定期模式来调用[计划自定义报告 API](schedule-a-new-report.md)。

4. 客户端应用程序还可以发送在已计划报告的数据准备就绪后要通知的回调 URL。

5. 成功时，“计划自定义报告 API”将返回 ReportID。

6. 在数据准备就绪可供定期下载后，回调 URL 会收到通知。

7. 然后，客户端应用程序通过[获取报告数据 API](get-report-data.md) 使用报告 ID 和日期范围来查询报告状态。

8. 成功时，会返回报告下载链接，并且应用程序可以启动数据下载。

9. 报告数据包含 CabIdHash，可以将其用作“Cab 下载 API”的输入来下载 cab 文件。

10. [Cab 下载 API](download-failure-cabs.md) 返回可以用来下载 cab 文件的 cab 下载链接。

## <a name="see-also"></a>另请参阅

- [创建新的报告模板](create-a-new-report-template.md)

- [示例报告模板](sample-report-templates.md)

- [分析报告 API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
