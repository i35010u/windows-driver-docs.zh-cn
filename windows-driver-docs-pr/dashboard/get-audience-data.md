---
title: 获取受众数据
description: Microsoft 硬件 API 中的这些方法可以获取要在发货标签中使用的组织的适用受众。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: 1e9aefd492d82db21cb8d1f851aedf5d8402c336
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "77072188"
---
# <a name="get-audience-data"></a>获取受众数据

在 *Microsoft 硬件 API* 中使用以下方法，获取适用于组织的受众。 受众允许你将发布限制为具有特定配置的计算机。 例如，测试部署只能传递给安装了特定注册表项的客户端。

```cpp
https://manage.devcenter.microsoft.com/v2.0/my/hardware/audiences
```

在使用这些方法之前，产品和提交必须已存在于你的开发人员中心帐户中。 若要创建或管理产品的提交内容，请参阅[管理产品提交内容](manage-product-submissions.md)中的方法。

|说明|方法|URI|
|-|-|-|
|获取适用于组织的受众列表。|GET|`https://manage.devcenter.microsoft.com/v2.0/my/hardware/audiences`|

## <a name="prerequisites"></a>必备条件

完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)（如果尚未这样做），然后尝试使用这其中的任何方法。

## <a name="data-resources"></a>数据资源

用于获取发货标签数据的 Microsoft 硬件 API 方法使用以下 JSON 数据资源。

### <a name="audience-resource"></a>受众资源

此资源表示适用于组织的受众。

```json
{
  "id": "9f4f44d8-bfec-48c6-a02c-2d9ea220f6e2",
  "name": "My Custom Audience",
  "description": "Matches machines that have the following registry key: HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\FOO-BAR",
  "audienceName": "Sample_Audience_Key"
}
```

此资源具有以下值

| 值 | 类型 | 说明 |
|:--|:--|:--|
|ID|字符串|受众的 ID。 这是将在发货标签中接收或发送的值。|
|name|字符串|受众的友好名称|
|description|字符串|受众的说明|
|audienceName|字符串|受众的名称|

## <a name="request"></a>请求

此方法具有以下语法。

|方法|请求 URI|
|--|--|
|GET|`https://manage.devcenter.microsoft.com/v2.0/my/hardware/audience`|

### <a name="request-header"></a>请求头

|Header|类型|说明|
|--|--|--|
|Authorization|字符串|必需。 Azure AD 访问令牌的格式为 **Bearer** *\<token\>* 。|
|accept|字符串|可选。 指定内容的类型。 允许的值是“application/json”|

### <a name="request-parameters"></a>请求参数

请勿为此方法提供请求参数。

### <a name="request-body"></a>请求正文

请勿为此方法提供请求正文。

### <a name="request-examples"></a>请求示例

以下示例演示了如何检索适用于组织的受众的相关信息。

```cpp
GET https://manage.devcenter.microsoft.com/v2.0/my/hardware/audience HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

以下示例演示了对适用于组织的所有受众的成功请求返回的 JSON 响应正文。 有关响应正文中的值的详细信息显示在示例后面的表中。

```json
{
  "value": [
    {
      "id": "9f4f44d8-bfec-48c6-a02c-2d9ea220f6e2",
      "name": "Test Registry Key",
      "description": "Matches machines that have the following registry key: HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\Test Drivers - use at own risk",
      "audienceName": "Test_Registry_Key"
    },
    {
      "id": "10415bba-3572-421b-a3de-d0d347bace5f",
      "name": "Test Audience 2",
      "description": "Additional Audeince",
      "audienceName": "Test_Audeince_2"
    }
  ],
  "links": [
    {
      "href": "https://manage.devcenter..microsoft.com/api/v1/hardware/audiences",
      "rel": "self",
      "method": "GET"
    }
  ]
}
```

此资源具有以下值

| 值 | 类型 | 说明 |
|:--|:--|:--|
| value | 数组 | 一个对象数组，其中包含有关每个受众的信息。 有关每个对象中的数据的详细信息，请参阅[受众资源](#audience-resource)。 |
| links | 数组 | 一个对象数组，其中包含有关包含实体的有用链接。 有关更多详细信息，请参阅[链接对象](get-product-data.md#link-object)。|

## <a name="see-also"></a>另请参阅

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
