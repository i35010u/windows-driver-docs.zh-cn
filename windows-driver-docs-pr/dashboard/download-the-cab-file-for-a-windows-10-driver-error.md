---
ms.assetid: 3D6EE7D7-7D75-499D-AA7A-55DA1C485BA6
description: 在 Microsoft Store 分析 API 中使用此方法，可下载 Windows 10 驱动程序错误的 CAB 文件。 此方法仅适用于 IHV。
title: 下载 Windows 10 驱动程序错误的 CAB 文件
ms.date: 08/28/2018
ms.topic: article
keywords: windows 10, uwp, Microsoft Store 分析 API, 下载 CAB
ms.localizationpriority: medium
ms.openlocfilehash: 9a7a534b4dc01d3d67ac4d4efda3e431868b4043
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353913"
---
# <a name="download-the-cab-file-for-a-windows-10-driver-error"></a>下载 Windows 10 驱动程序错误的 CAB 文件

> [!IMPORTANT]
> 本主题包含已弃用的材料。 它介绍了用于收集驱动程序提交失败相关数据的旧方法。 它仅为支持旧版提供。
>
> 请改为参考这些更新的主题：
>
> - [计划自定义报告以获取驱动程序失败详细信息](schedule-custom-reports-for-driver-failure-details.md)
> - [创建新的报告模板](create-a-new-report-template.md)
> - [计划新报告](schedule-a-new-report.md)
> - [获取报告数据](get-report-data.md)

在 Microsoft Store 分析 API 中使用此方法，可下载与特定 Windows 10 驱动程序错误相关的 CAB 文件。 开始使用此方法之前，必须先使用[获取 Windows 10 驱动程序错误的详细信息](get-details-for-a-windows-10-driver-error.md)方法来检索要下载的 CAB 文件的 ID。

可以在 Microsoft Store 分析 API 中使用[获取 Windows 10 驱动程序的错误报告数据](get-error-reporting-data-for-windows-10-drivers.md)和[获取 Windows 10 驱动程序错误的详细信息](get-details-for-a-windows-10-driver-error.md)方法来获取有关 OEM 硬件错误的其他信息。

> [!NOTE]
> 此方法仅可供属于[合作伙伴中心计划](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-started-with-the-hardware-dashboard)的开发者帐户使用。

## <a name="prerequisites"></a>必备条件

若要使用此方法，首先需要执行以下操作：

- 完成 Microsoft Store 分析 API 的所有[先决条件](https://docs.microsoft.com/windows/uwp/monetize/access-analytics-data-using-windows-store-services#prerequisites)（如果尚未这样做）。

- [获取 Azure AD 访问令牌](https://docs.microsoft.com/windows/uwp/monetize/access-analytics-data-using-windows-store-services#obtain-an-azure-ad-access-token)，以供在此方法的请求标头中使用。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。

- 获取要下载的 CAB 文件的 ID。 若要获取此 ID，请使用[获取 Windows 10 驱动程序错误的详细信息](get-details-for-a-windows-10-driver-error.md)方法来检索特定驱动程序错误的详细信息，并使用该方法的响应正文中的 **cabIdHash** 值。

## <a name="request"></a>请求

### <a name="request-syntax"></a>请求语法

| 方法 | 请求 URI                                                          |
|--------|----------------------------------------------------------------------|
| GET    | `https://manage.devcenter.microsoft.com/v1.0/my/analytics/driver/cabdownload` |

### <a name="request-header"></a>请求头

| 标头        | 在任务栏的搜索框中键入   | 描述                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** *token*&lt;&gt;。 |

### <a name="request-parameters"></a>请求参数

| 参数        | 在任务栏的搜索框中键入   |  描述      |  必需  |
|---------------|--------|---------------|------|
| applicationId | 字符串 | 要为其检索错误数据的驱动程序的产品 ID 值。 |  是  |
| cabIdHash | 字符串 | 要下载的 CAB 文件的唯一 ID。 若要获取此 ID，请使用[获取 Windows 10 驱动程序错误的详细信息](get-details-for-a-windows-10-driver-error.md)方法来检索应用中特定错误的详细信息，并使用该方法的响应正文中的 **cabIdHash** 值。 |  是  |

### <a name="request-example"></a>请求示例

以下示例演示如何使用此方法下载 CAB 文件。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/driver/cabdownload?applicationId=18430592857500421&cabIdHash=c1a51104-d682-4230-be14-7278b18e3555 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

此方法将会返回一个 302（重定向）响应代码，并且会将响应中的 **Location** 标头分配给 CAB 文件的共享访问签名 (SAS) URI。 调用程序将被重定向至此 URI 以自动下载 CAB 文件。

## <a name="related-topics"></a>相关主题

- [获取 Windows 10 驱动程序的错误报告数据](get-error-reporting-data-for-windows-10-drivers.md)
- [获取 Windows 10 驱动程序错误的详细信息](get-details-for-a-windows-10-driver-error.md)
