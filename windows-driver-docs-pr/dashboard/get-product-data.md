---
title: 获取产品数据
description: Microsoft 硬件 API 中的这些方法可获取注册到开发人员中心帐户的硬件产品的数据。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: b1c3c7b756f570bd1775d874988cf38b6827f092
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518510"
---
# <a name="get-product-data"></a>获取产品数据

使用 Microsoft 硬件 API 中的以下方法可获取注册到开发人员中心帐户的硬件产品的数据。 有关 Microsoft 硬件 API 的简介，包括关于使用 API 的先决条件的简介，请参阅[使用 API 管理硬件提交](dashboard-api.md)。

```cpp
https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/
```

在使用这些方法之前，产品必须已存在于你的开发人员中心帐户中。 若要创建或管理产品提交，请参阅[管理产品提交](manage-product-submissions.md)中的方法。

| 方法 | URI | 描述 |
|-|-|-|
|GET |`https://manage.devcenter.microsoft.com/v1.0/hardware/products/`|[获取所有产品的数据](get-all-products.md)|
|GET |`https://manage.devcenter.microsoft.com/v1.0/hardware/products/{productID}`|[获取某个特定产品的数据](get-a-product.md)|
|GET |`https://manage.devcenter.microsoft.com/v1.0/hardware/products/{productID}/submissions`|[获取产品的所有提交的数据](get-all-submissions.md)|
|GET |`https://manage.devcenter.microsoft.com/v1.0/hardware/products/{productID}/submissions/{submissionId}`|[获取产品的特定提交的数据](get-a-submission.md)|

## <a name="prerequisites"></a>必备条件

完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)（如果尚未这样做），然后尝试使用这其中的任何方法。

## <a name="data-resources"></a>数据资源

用于获取产品数据的 Microsoft 硬件 API 方法使用以下 JSON 数据资源

### <a name="product-resource"></a>产品资源

此资源表示已注册到你的帐户的硬件产品（驱动程序）。

```json
{
  "id”: 9007199267351834,
  “sharedProductId”: 1152921504606971100,
  “links”: [
    {
      “href": "https:// manage.devcenter.microsoft.com/api/v1.0/hardware/products/9007199267351834",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https:// manage.devcenter.microsoft.com/api/v1.0/hardware/products/9007199267351834/submissions",
      "rel": "get_submissions",
      "method": "GET"
    }
  ],
  "isCommitted": true,
  "isExtensionInf": false, "_comment": "THis field is deprecated and moved to submission resource",
  "deviceMetadataIds": [],
  "deviceType": "notSet",
  "isTestSign": false,
  "isFlightSign": false,
  "marketingNames": [
    "marketing name 1",
    " marketing name 2"
],
  "productName": "product name",
  "selectedProductTypes": {
    "windows_v100Server": "Unclassified",
    "windows_v100": "Unclassified"
},
  "requestedSignatures": [
    "WINDOWS_v100_X64_TH1_FULL",
    "WINDOWS_v63_X64"
  ],
  "additionalAttributes": {},
  "testHarness": "hlk",
  " announcementDate ": "2016-10-22T00:00:00Z",
}
```

此资源具有以下值

| 值 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| ID | Long | 产品的专用产品 ID |
| sharedProductId | Long | 产品的共享产品 ID |
| 链接 | 对象数组 | 有关更多详细信息，请参阅[链接对象](#link-object) |
| isCommitted | 布尔 | 指示产品是否至少有一个确认的提交  |
| isExtensionInf | 布尔 | （已弃用）指示产品是否为扩展驱动程序。 此字段已弃用，不应再使用。 isExtensionInf 已移至提交级别属性。 |
| deviceMetadataIds | GUID 数组 | 将设备元数据提交映射到驱动程序的 GUID |
| deviceType | 字符串 | 指示设备的类型。 可能的值为：<ul><li>“internal”- 内部组件，设备是系统的一部分，在电脑内部进行连接</li><li>“external”- 外部组件，设备是连接到电脑的外部设备（外设）</li><li>“internalExternal”- 两者，设备可以在内部（在电脑内）和外部（外设）进行连接</li><li>“notSet”- 没有可用数据</li></ul>|
| isTestSign | 布尔 | 指示产品是否为经过测试签名的驱动程序。 有关对驱动程序包进行测试签名的详细信息，请参阅 [WHQL Test Signature Program](https://docs.microsoft.com/windows-hardware/drivers/install/whql-test-signature-program)（WHQL 测试签名计划）  |
| isFlightSign | 布尔 | 指示产品是否为经过外部测试签名的驱动程序。 经过外部测试签名的驱动程序是指可以通过 Windows 更新发布的测试驱动程序。 它们只能发布/安装在已注册 Windows 预览体验计划的计算机上。 它们可以在不禁用安全启动的情况下安装在计算机上。 它们不能安装在未加入 Windows 预览体验计划的零售计算机上。|
| marketingNames | 字符串数组 | 产品的营销名称或别名 |
| productName | 字符串 | 在创建期间指定的驱动程序的名称 |
| selectedProductTypes | 字典  | 均为字符串的键值对。 <ul><li>**键**表示操作系统系列代码。 有关操作系统系列代码的列表，请参阅[操作系统系列代码列表](#list-of-operating-system-family-codes)。</li><li>**值**表示产品的类型。 有关产品类型的列表，请参阅[产品类型](#list-of-product-types)。</li></ul>|
| requestedSignatures | 字符串数组 | 产品通过认证的操作系统签名的列表。 有关所有操作系统的列表，请参阅[操作系统代码列表](#list-of-operating-system-codes)  |
| additionalAttributes | 对象 | 有关更多详细信息，请参阅[附加属性对象](#additional-attribute-object)。 |
| testHarness | 字符串 | 已提交的程序包的类型。 可能的值为 <ul><li>hlk<li>hck</li><li>attestation</li><li>notset</li></ul>|
| announcementDate | 日期/时间 | 产品将包含在 Windows Server Catalog 中的日期 |

### <a name="submission-resource"></a>提交资源

此资源表示产品的提交。

```json
{
  "id": 1152921504621442000,
  "productId": 13635057453741328,
   "workflowStatus": {
      “currentStep": " finalizeIngestion",
      " state": " completed",
      " messages": []
    },
  "links": [
    {
      "href": "https:// manage.devcenter.microsoft.com/api/v1.0/hardware/products/13635057453741329/submissions/1152921504621441944",
      "rel": "self",
      "method": "GET"
    }
  ],
  "commitStatus": "commitPending",
  "isExtensionInf": true,
  "isUniversal": true,
  "isDeclarativeInf": true,
  "name": "HARRY-Duatest2",
  "type": "derived"
}
```

此资源具有以下值

| 值 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| ID | 长整型 | 提交的 ID |
| Productid | 长整型 | 与此提交关联的专用产品 ID |
| 链接 | 对象数组 | 有关更多详细信息，请参阅[链接对象](#link-object) |
| 名称 | 字符串 | 提交的名称 |
| 在任务栏的搜索框中键入 | 字符串 | 指示提交是初始提交还是派生的提交。 可能的值为 <ul><li>initial</li><li>derived</li></ul> |
| isExtensionInf | 布尔 | 指示提交是否为扩展驱动程序 |
| isUniversal | 布尔 | 指示提交是否通过通用 API 测试。 如果驱动程序是声明性的并且可以通用，则表明它符合 DCHU 的标准 |
| isDeclarativeInf | 布尔 | 指示提交是否通过声明性 INVerif 测试。 如果驱动程序是声明性的并且可以通用，则表明它符合 DCHU 的标准 |
| workflowstatus | 对象 | 此项仅在检索特定提交的详细信息时可用。 此对象描述此提交的工作流状态。 有关更多详细信息，请参阅[工作流状态对象](#workflow-status-object)  |
| downloads | 对象 | 此项仅在只检索特定提交的详细信息时可用。 此对象描述可用于提交的下载。 有关更多详细信息，请参阅[下载对象](#download-object)。 |

### <a name="workflow-status-object"></a>工作流状态对象

此对象表示给定实体的工作流状态

```json
{
      “currentStep": " finalizeIngestion",
      " state": " completed",
      " messages": []
    }
```

此对象具有以下值

| 值 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| currentStep | 字符串 | 此实体的整个工作流中的当前步骤名称。 <br>对于引入/程序包提交，可能的值为（括号中的内容为说明）：<ul><li>packageInfoValidation（验证程序包元数据和内容）</li><li>preparation（准备好程序包以便进行处理）</li><li>scanning（扫描程序包内容中是否有恶意软件）</li><li>validation（验证测试结果）</li><li>catalogCreation（为程序包创建安全目录）</li><li>manualReview（进行手动审查）</li><li>signing（对二进制文件签名）</li><li>finalizeIngestion（完成引入并获取可以下载或发布的签名文件）</li></ul>|
| 状态 | 字符串 | 当前步骤的状态。 可能的值为：<ul><li>notStarted</li><li>started</li><li>失败</li><li>completed</li></ul> |
| Messages | 数组 | 一个字符串数组，用于提供有关当前步骤的消息（尤其是在失败的情况下） |

### <a name="download-object"></a>下载对象

此对象表示给定提交的下载。

```json
{
  "items": [
    {
      "type": "initialPackage",
      "url": "https://ingestionpackagesint1.blob.core.windows.net/ingestion/dc55b8c6-a01c-40b6-b815-cac8bc08812a?sv=2016-05-31&sr=b&sig=ipjW3RsVC75lZrcEZRh9JmTX89L4gTIKkxwqv9F8Axs%3D&se=2018-03-12T15:32:10Z&sp=rl"
    },
    {
      "type": "derivedPackage",
      "url": "https://ingestionpackagesint1.blob.core.windows.net/ingestion/6bd77dbf-a851-46d2-b703-29ea4efae006?sv=2016-05-31&sr=b&sig=O5XQf%2FzMbI2FFt5WwSUJWL1JbWY4JXXPRkCKAnX7IRs%3D&se=2018-03-12T15:32:10Z&sp=rl&rscd=attachment%3B filename%3DShell_1152921504621441930.hlkx"
    },
    {
      "type": "signedPackage",
      "url": "https://ingestionpackagesint1.blob.core.windows.net/ingestion/0b83a294-c1d1-4136-82a1-dd52f51841e3?sv=2016-05-31&sr=b&sig=zTfxKJmaTwpbFol%2FpAKG0QuXJTTxm5aZ0F2wQQI8whc%3D&se=2018-03-12T15:32:10Z&sp=rl"
    },
    {
      "type": "certificationReport",
      "url": "https:// manage.devcenter.microsoft.com/dashboard/hardware/Driver/DownloadCertificationReport/29963920/13635057453741329/1152921504621441930"
    }
  ],
  "messages": []
}
```

此对象具有以下值

| 值 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| 项目 | 数组 | 下载类型和每种类型的 URL 的数组。 有关详细信息，请参阅下文 |
| 在任务栏的搜索框中键入 | 字符串 | 可供下载的程序包的类型。 可能的值为：<ul><li>“initialPackage”- 用户上传的程序包（对于新提交，它指向用于上传程序包的 SAS URI）</li><li>“derivedPackage”- 派生的提交的 Shell</li><li>“signedPackage”- 由 Microsoft 签名的程序包</li><li>“certificationReport”- 签名产品的认证报告</li></ul>|
| Messages | 数组 | 一个字符串数组，用于提供有关可下载文件的消息 |

### <a name="link-object"></a>链接对象

此对象表示包含实体的帮助链接的列表

```json
{
      “href": "https:// manage.devcenter.microsoft.com/api/v1.0/hardware/products/9007199267351834",
      "rel": "self",
      "method": "GET"
    }
```

此对象具有以下值

| 值 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| Href | 字符串 | 通过 API 访问资源的 URL |
| Rel | 字符串 | 资源的类型。 可能的值为：<ul><li>self - 链接指向自身</li><li>next_link - 链接指向通常用于分页的下一个资源</li><li>get_submissions - 链接指向产品的所有提交</li><li>commit_submission - 链接指向提交的确认 </li><li>update_submission - 链接指向提交的更新 </li><li>update_shippinglabel - 链接指向发货标签的更新  </li><li>driverMetadata - 链接指向用于下载驱动程序元数据的文件。 有关更多详细信息，请参阅[驱动程序包元数据](driver-package-metadata.md)。</li></ul>|
| 方法 | 字符串 | 调用 URL 时要使用的 http 方法的类型。 可能的值为<ul><li>GET</li><li>POST</li><li>修补程序</li></ul>|

### <a name="additional-attribute-object"></a>附加属性对象

如果产品的类型是 RAID 控制器、存储控制器或服务器虚拟化验证计划 (SVVP)，则此对象提供有关产品的附加属性。 它可能包含 StorageController、RaidController、SVVP 这三种对象类型中的一种。

#### <a name="storagecontroller-object"></a>StorageController 对象

| 值 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| biosVersion | 字符串 | ROM Bios 版本 |
| firmwareVersion | 字符串 | 固件版本 |
| driverVersion | 字符串 | 驱动程序版本 |
| driverName | 字符串 | 驱动程序名称 |
| deviceVersion | 字符串 | 设备版本 |
| chipsetName | 字符串 | 芯片组名称 |
| usedProprietary | 布尔值 | 通过专用驱动程序支持的多路径。 如果为 true，则 proprietaryName 和 proprietaryVersion 是必需项 |
| proprietaryName | 字符串 | 多路径软件名称 |
| proprietaryVersion | 字符串 | 多路径软件版本 |
| usedMicrosoft | 布尔值 | 通过特定于设备的模块支持的 Microsoft MPIO。 如果为 true，则 microsoftName 和 microsoftVersion 是必需项 |
| microsoftName | 字符串 | 多路径软件名称 |
| microsoftVersion | 字符串 | 多路径软件版本 |
| usedBootSupport | 布尔值 | 启动支持 |
| usedBetterBoot | 布尔值 | 支持启动 >2.2TB。  如果为 true，则支持的 UEFI 版本和支持的 ACPI 版本是必需项 |
| uefiVersion | 字符串 | 支持的 UEFI 版本 |
| acpiVersion | 字符串 | 支持的 ACPI 版本 |
| supportsSector4K512E | 布尔值 | 支持 4K/512e 扇区大小 |
| supportsSector4K4K | 布尔值 | 支持 4K/4K 扇区大小 |
| supportsDifferential | 布尔值 | 差分（高压差分） |

#### <a name="raidcontroller-object"></a>RaidController 对象

| 值 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| firmwareVersion | 字符串 | 固件版本 |
| filterVersion | 字符串 | 驱动程序版本 |
| driverVersion | 字符串 | 筛选器版本 |
| usedProprietary | 布尔值 | 通过专用驱动程序支持的多路径。 如果为 true，则 proprietaryName 和 proprietaryVersion 是必需项 |
| proprietaryName | 字符串 | 多路径软件名称 |
| proprietaryVersion | 字符串 | 多路径软件版本 |
| usedMicrosoft | 布尔值 | 通过特定于设备的模块支持的 Microsoft MPIO。 如果为 true，则 microsoftName 和 microsoftVersion 是必需项 |
| microsoftName | 字符串 | 多路径软件名称 |
| microsoftVersion | 字符串 | 多路径软件版本 |
| isThirdPartyNeeded | 布尔值 | 进行连接所需的第三方非 Microsoft 驱动程序 |
| isSES | 布尔值 | SES (SCSI Enclosure Services)。 指示是否包含 SES。 SCSI 是连接系统设备的服务总线的标准术语，最初是指 Small Computer System Interface（小型计算机系统接口）。 SES 是 SCSI Enclosure Services 的简称。 |
| isSAFTE | 布尔值 | SAF-TE（ANBll 规范）。 指示是否包含 SAF-TE。 ANBll 是一项行业规范。 SAF-TE 是 SCSI Accessed Fault Tolerant Enclosures 的简称。 SCSI 是连接系统设备的服务总线的标准术语，最初是指 Small Computer System Interface（小型计算机系统接口）。 |
| additionalInfo | 字符串 | 其他信息 |

#### <a name="svvp-object"></a>SVVP 对象

| 值 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| productVersion | 字符串 | 产品版本 |
| supportLink | 字符串 | 支持 URL |
| guestOs | 字符串 | 来宾操作系统。 可能的值为：<ul><li>Windows Server 2008</li><li>Windows Server 2008 Release 2</li><li>Windows Server 2012</li><li>Windows Server 2012 R2 </li></ul>|
| processorArchitecture | 字符串 | 硬件处理器体系结构。 可能的值为：<ul><li>Xeon</li><li>Opteron</li><li>Itanium 2</li></ul>|
| maxProcessors | 整数 | 虚拟机中的最大处理器数 |
| maxMemory | 整数 | 虚拟机中的最大内存（以 GB 为单位） |

### <a name="list-of-product-types"></a>产品类型列表

产品可以是以下类型。 该信息与操作系统一起用于确定适用性。

* 一体机
* 触控一体机
* 音频设备
* 蓝牙控制器
* 蓝牙控制器（非 USB）
* 可变式平板电脑
* 桌面设备
* 数字媒体呈现器
* 数字媒体服务器
* 数码相机
* 数字视频摄像机
* 支持分布式扫描管理的设备
* 企业 WSD 多功能打印机
* 指纹读取器
* 游戏控制器
* 通用控制器
* 通用便携设备
* 图形适配器 WDDM1.0
* 图形适配器 WDDM1.1
* 图形适配器 WDDM1.2
* 图形适配器 WDDM1.2 DisplayOnly
* 图形适配器 WDDM1.2 RenderOnly
* 图形平板电脑
* 硬盘驱动器
* 键盘
* 键盘、视频、鼠标开关
* LAN
* LAN（服务器）
* LAN CS
* LAN 虚拟机（服务器）
* 便携式计算机
* 触控式笔记本电脑
* LCD
* 光传感器
* 位置传感器
* 媒体播放器
* 移动宽带 CDMA
* 移动宽带 GSM
* 移动电话
* 监视器
* 母板
* 运动传感器融合
* 多功能打印机
* 近场近程
* 网络媒体设备
* 光驱
* 触控笔数字化器
* 指向绘图
* 存在传感器
* 打印机
* Projector
* 可移动存储
* 路由器
* 扫描仪
* SDIO 控制器
* Server
* 服务器虚拟化验证计划
* 签名平板电脑
* 智能卡
* 智能卡读卡器
* 存储阵列
* 存储控制器
* 存储空间适配器
* 存储空间驱动器
* Tablet
* 触控
* 触控监视器
* 超级移动电脑
* 触控式超级移动电脑
* USB 控制器
* USB 集线器
* 网络摄像头
* WLAN
* WLAN CSB
* WSD 多功能打印机
* WSD 打印机
* WSD 扫描仪

### <a name="list-of-operating-system-family-codes"></a>操作系统系列代码列表

下表列出了操作系统系列代码及其说明。

| 操作系统系列代码 | 描述 |
|:--|:--|
| WindowsMe | Windows Me |
| Windows2000 | Windows 2000 |
| Windows98 | Windows 98 |
| WindowsNT40 | Windows NT 4.0 |
| WindowsXP | Windows XP |
| WindowsServer2003 | Windows Server 2003 |
| WindowsVista | Windows Vista |
| Windows2008Server | Windows Server 2008 |
| WindowsHomeServer | Windows Home Server |
| Windows7 | Windows 7 |
| Windows2008ServerR2 | Windows Server 2008 Release 2 |
| WindowsServerSolutions | Windows Server 解决方案 |
| Windows8 | Windows 8 |
| Windows8Server | Windows Server 2012 |
| Windows81 | Windows 8.1 |
| Windows81Server | Windows Server 2012 R2 |
| Windows_v100 | Windows 10 Threshold |
| Windows_v100Server | Windows Server Threshold |
| Windows_v100_RS1 | Windows 10 周年更新 |
| Windows_v100Server_RS1 | Windows Server 2016 |
| Windows_v100_RS2 | Windows 10 RS2 更新 |
| Windows_v100Server_RS2 | Windows Server RS2 |
| Windows_v100_RS3 | Windows 10 RS3 更新 |
| Windows_v100Server_RS3 | Windows Server RS3 |
| Windows_v100_RS4 | Windows 10 RS4 更新 |
| Windows_v100Server_RS5 | Windows Server 2019 |
| Windows_v100_RS5 | Windows 10 RS5 x86 |
| Windows_v100_RS5 | Windows 10 RS5 x64 |

### <a name="list-of-operating-system-codes"></a>操作系统代码列表

下表列出了操作系统代码及其说明。

| 操作系统代码 | 描述 |
|:--|:--|
|WINDOWS_ME|Windows Me|
|WINDOWS_98|Windows 98|
|WINDOWS_2000|Windows 2000|
|WINDOWS_NT40|Windows NT 4.0|
|WINDOWS_XP|Windows XP|
|WINDOWS_XP_IA64|Windows XP IA64|
|WINDOWS_XP_X64|Windows XP X64|
|WINDOWS_XP_MEDIA_CENTER|Windows XP Media Center|
|WINDOWS_2003|Windows Server 2003|
|WINDOWS_2003_IA64|Windows Server 2003 IA64|
|WINDOWS_2003_X64|Windows Server 2003 X64|
|WINDOWS_VISTA|Windows Vista 客户端|
|WINDOWS_VISTA_X64|Windows Vista 客户端 X64|
|WINDOWS_2008_SERVER|Windows Server 2008|
|WINDOWS_2008_SERVER_IA64|Windows Server 2008 IA64|
|WINDOWS_2008_SERVER_X64|Windows Server 2008 X64|
|WINDOWS_HOME_SERVER|Windows Home Server|
|WINDOWS_7|Windows 7 客户端|
|WINDOWS_7_X64|Windows 7 客户端 x64|
|WINDOWS_2008_SERVER_R2_IA64|Windows Server 2008 Release 2 IA64|
|WINDOWS_2008_SERVER_R2_X64|Windows Server 2008 Release 2 x64|
|WINDOWS_SERVER_SOLUTIONS_X64|Windows Server 解决方案 x64|
|WINDOWS_8|Windows 8 客户端|
|WINDOWS_8_X64|Windows 8 客户端 x64|
|WINDOWS_8_ARM|Windows 8 客户端 RT|
|WINDOWS_8_SERVER_X64|Windows Server 2012|
|WINDOWS_v63|Windows 8.1 客户端|
|WINDOWS_v63_X64|Windows 8.1 客户端 x64|
|WINDOWS_v63_ARM|Windows 8.1 客户端 RT|
|WINDOWS_v63_SERVER_X64|Windows Server 2012 R2 x64|
|WINDOWS_v100_TH1_FULL|Windows 10 客户端版本 1506 和 1511 (TH1)|
|WINDOWS_v100_X64_TH1_FULL|Windows 10 客户端版本 1506 和 1511 x64 (TH1)|
|WINDOWS_v100_SERVER_X64_TH1_FULL|Windows Server 2016 x64 (TH1)|
|WINDOWS_v100_TH2_FULL|Windows 10 客户端版本 1506 和 1511 (TH2)|
|WINDOWS_v100_X64_TH2_FULL|Windows 10 客户端版本 1506 和 1511 x64 (TH2)|
|WINDOWS_v100_SERVER_X64_TH2_FULL|Windows Server 2016 x64 (TH2)|
|WINDOWS_v100_RS1_FULL|Windows 10 客户端版本 1607|
|WINDOWS_v100_X64_RS1_FULL|Windows 10 客户端版本 1607 x64|
|WINDOWS_v100_SERVER_X64_RS1_FULL|Windows Server 2016 x64 (RS1)|
|WINDOWS_v100_RS2_FULL|Windows 10 RS2 客户端|
|WINDOWS_v100_X64_RS2_FULL|Windows 10 RS2 客户端 x64|
|WINDOWS_v100_RS3_FULL|Windows 10 RS3 客户端|
|WINDOWS_v100_X64_RS3_FULL|Windows 10 RS3 客户端 x64|
|WINDOWS_v100_ARM64_RS3_FULL|Windows 10 RS3 客户端 ARM64|
|WINDOWS_v100_RS4_FULL|Windows 10 RS4 客户端|
|WINDOWS_v100_X64_RS4_FULL|Windows 10 RS4 客户端 x64|
|WINDOWS_v100_ARM64_RS4_FULL|Windows 10 RS4 客户端 ARM64|
| WINDOWS_v100_SERVER_X64_RS5_FULL | Windows Server 2019 |
| WINDOWS_v100_RS5_FULL | Windows 10 RS5 x86 |
| WINDOWS_v100_X64_RS5_FULL | Windows 10 RS5 x64 |

## <a name="error-codes"></a>错误代码

错误代码适用于 API 的所有 Web 方法。 如果无法成功完成请求，该响应中会包含以下 HTTP 错误代码之一。

| HTTP 状态 | 描述 |
|:--|:--|
| 400 - 错误请求 | 请求格式不正确（例如，请求语法格式错误、请求消息帧无效或请求路由具有欺骗性） |
| 401 - 未授权 | 身份验证失败或未提供 |
| 403 - 已禁止 | 禁止访问资源 |
| 404 - 未找到 | 找不到请求的实体。 |
| 415 - 不支持的媒体类型 | 在目标资源上，此方法不支持有效负载的格式。 |
| 422 - 无法处理的实体 | 验证失败。 |
| 500 - 内部服务器错误 | API 服务器中出现无法恢复的错误。 |


如果功能验证失败，则响应正文将包含以下其中一个功能错误代码。

| 错误代码 | 错误消息 | 描述 |
|:--|:--|:--|
| InvalidInput |  | 输入验证失败时返回此项 |
| RequestInvalidForCurrentState | 只能确认待定提交 | 对未处于待定状态的提交应用确认时返回此项 |
| RequestInvalidForCurrentState | 初始提交已存在 | 为已有初始提交的驱动程序创建初始提交时返回此项 |
| RequestInvalidForCurrentState | 由于没有创建初始提交，因此无法创建派生提交 | 为没有初始提交的驱动程序创建派生提交时返回此项 |
| UpdateUnauthorized | 无权更新产品 | 尝试更新共享（转售）的产品时返回此项，因为无法更新共享的产品 |
| UpdateUnauthorized | 在没有初始提交的情况下无法更新产品 | 尝试更新没有初始提交的产品时返回此项 |
| UpdateUnauthorized | 工作流失败，因此无法更新产品 | 尝试更新工作流失败的产品时返回此项 |
| UpdateUnauthorized | 引入过程完成后不能更新公告日期 | 引入完成后更新公告日期时返回此项 |
| UpdateUnauthorized | 此时无法更新产品名称。 请重试 |  |
| UpdateUnauthorized | 无权更新提交 | 尝试更新共享（转售）的产品的提交时返回此项，因为无法更新共享的产品 |
| UpdateUnauthorized | 由于工作流失败，因此无法更新提交 | 尝试更新工作流失败的提交时返回此项 |
| EntityNotFound | 未找到提交 | 尝试确认不存在的提交时返回此项 |
| EntityNotFound | 找不到产品 | 尝试创建产品不存在的提交时返回此项 |
| InvalidInput | 扩展驱动程序必须作为自动更新发布。 isAutoInstallDuringOSUpgrade 或 isAutoInstallOnApplicableSystems 必须为 true。 | 在不选择 isAutoInstallDuringOSUpgrade 或 isAutoInstallOnApplicableSystems 的情况下为扩展 INF 创建 Windows 更新发货标签时返回此项 |
| InvalidInput | 只有在 HardwareId 是用于 Windows10 及更高版本的操作系统时才允许 Chid。 | 如果在启用 CHID 目标设定的情况下创建一个发货标签，且该标签针对的操作系统低于 Windows 10，则会返回此项。 CHID 目标设定仅适用于 Windows 10 及更高版本。 |
| InvalidInput | 当另一工作流正在进行的时候，不能更新发货标签。 请重试。 | 当前面的某个工作流仍在进行的时候，如果更新发货标签，则会返回此项。 |
| RequestInvalidForCurrentState | 不能为收件箱或系统类型创建“发布”发货标签。 只能共享发货标签。 | 在收件箱驱动程序或系统上创建 Windows 更新发货标签时返回此项。 |
| RequestInvalidForCurrentState | 提交尚未做好创建发货标签的准备。 请过一段时间后重试。 | 如果在创建发货标签时不需等待准备或预先处理完成，则返回此项。 |

## <a name="see-also"></a>另请参阅

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
