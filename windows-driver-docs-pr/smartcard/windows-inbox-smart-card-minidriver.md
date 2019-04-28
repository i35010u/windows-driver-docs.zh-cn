---
title: Windows 收件箱智能卡微型驱动程序
description: Windows 收件箱智能卡微型驱动程序
ms.assetid: 4B61607E-090A-4935-B944-110ACE9A4D83
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b6711bb48a2a0e4b81067fa734c26fcbd2c8ca5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348124"
---
# <a name="windows-inbox-smart-card-minidriver"></a>Windows 收件箱智能卡微型驱动程序


从 Windows 7 Service Pack 1 (SP1) 开始，提供的支持符合 piv 标准的智能卡和实现 GID 卡边缘的卡，收件箱泛型类微型驱动程序。

符合 piv 标准的智能卡和卡实现 GID 纸牌的边缘。 有关 piv 标准的详细信息，请参阅[有关个人标识验证 (PIV) 联邦员工和合同工的](http://csrc.nist.gov/groups/SNS/piv/index.mdl)网页。

有关 GID 的详细信息，请参阅[通用标识设备规范](https://msdn.microsoft.com/windows/hardware/gg487496)网页。

智能卡插入读取器和基本 CSP/KSP 时调用[ **CardAcquireContext**](https://msdn.microsoft.com/library/windows/hardware/dn468701)，类微型驱动程序将执行以下的发现过程，以将标记为任一 PIV-关联的卡或GID 合规：

1.  发出 SELECT 命令来查找 PIV 辅助设备。 如果命令成功，Windows 会考虑卡为 PIV 设备和发现过程停止。
2.  如果该命令将失败，则发出 SELECT 命令以找到 GID 辅助设备。 如果命令成功，Windows 会考虑卡为 GID 设备和发现过程停止。
3.  如果命令失败，状态代码，以指示既不帮助存在智能卡上，Windows 仍将继续像卡是 GID 设备。 如果该命令将失败，任何其他错误，Windows 会考虑卡是一个未知的设备。

## <a name="span-idelectricalprofileforgidscardswiththemicrosoftgenericprofilespanspan-idelectricalprofileforgidscardswiththemicrosoftgenericprofilespanspan-idelectricalprofileforgidscardswiththemicrosoftgenericprofilespanelectrical-profile-for-gids-cards-with-the-microsoft-generic-profile"></a><span id="Electrical_Profile_for_GIDS_cards_with_the_Microsoft_Generic_Profile"></span><span id="electrical_profile_for_gids_cards_with_the_microsoft_generic_profile"></span><span id="ELECTRICAL_PROFILE_FOR_GIDS_CARDS_WITH_THE_MICROSOFT_GENERIC_PROFILE"></span>与 Microsoft 的泛型配置文件电气 GID 卡的配置文件


智能卡的实现 GID 卡边缘上，它们必须是带电气配置文件，使其使用收件箱类微型驱动程序为预配预配。 在本部分中的信息需要深入了解 Apdu、 数据模型和 GID 规范中指定的卡边缘。

此处提供的子节的后面必须前卡可用于个性化设置列出的顺序。 请参阅此部分中提到的 Apdu 的详细信息的 GID 规范的部分 11。

### <a name="span-idgidsapplicationmetadataspanspan-idgidsapplicationmetadataspanspan-idgidsapplicationmetadataspangids-application-metadata"></a><span id="GIDS_Application_Metadata"></span><span id="gids_application_metadata"></span><span id="GIDS_APPLICATION_METADATA"></span>GID 应用程序元数据

在本部分中所述的 DOs GID 由管理，可以仅在 SELECT 命令的响应数据字段中检索。 在应用程序"创建"状态时，只能创建此元数据。 请有关详细信息 GID 生命周期管理 GID 规范的第 6 节，参阅。

请注意，下面提供了元数据仅包含存在完全按所述 （除非另有说明） 的要求。 有可能是可选的也是可自定义卡应用程序供应商的其他字段。

### <a name="span-idfilecontrolinformationdffcispanspan-idfilecontrolinformationdffcispanspan-idfilecontrolinformationdffcispan-file-control-information-df-fci"></a><span id="_File_Control_Information__DF_FCI_"></span><span id="_file_control_information__df_fci_"></span><span id="_FILE_CONTROL_INFORMATION__DF_FCI_"></span> 文件控制信息 (DF FCI)

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Tag</th>
<th align="left">Len</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">64</td>
<td align="left">Var。</td>
<td align="left"><p>应用程序模板数据对象</p>
<p></p>
<dl>
<dt><span id="Tag"></span><span id="tag"></span><span id="TAG"></span>标记</dt>
<dd><p>4F</p>
</dd>
<dt><span id="Len"></span><span id="len"></span><span id="LEN"></span>Len</dt>
<dd><p>Var。</p>
</dd>
<dt><span id="Value"></span><span id="value"></span><span id="VALUE"></span>值</dt>
<dd><p>应用程序的辅助工具 =</p>
<p>A0 00 00 03 97 42 54 46 59 xx yy</p>
<ul>
<li><strong>XX</strong> = 01 或 02 GID 规范修订号。</li>
<li><strong>YY</strong> = 保留以卡应用程序。</li>
</ul>
</dd>
</dl></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfilemanagementdatadffmdspanspan-idfilemanagementdatadffmdspanspan-idfilemanagementdatadffmdspan-file-management-data-df-fmd"></a><span id="_File_Management_Data__DF_FMD_"></span><span id="_file_management_data__df_fmd_"></span><span id="_FILE_MANAGEMENT_DATA__DF_FMD_"></span> 文件管理数据 (DF FMD)

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Tag</th>
<th align="left">Len</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">64</td>
<td align="left">Var。</td>
<td align="left"><p>FMD 模板</p>
<p></p>
<dl>
<dt><span id="Tag"></span><span id="tag"></span><span id="TAG"></span>标记</dt>
<dd><p>5F2F</p>
</dd>
<dt><span id="Len"></span><span id="len"></span><span id="LEN"></span>Len</dt>
<dd><p>Var。</p>
</dd>
<dt><span id="Value"></span><span id="value"></span><span id="VALUE"></span>值</dt>
<dd><p>PIN 使用情况策略 （请参阅"PIN 使用情况策略"） =</p>
<p>40 或 60</p>
<ul>
<li><strong>40</strong> – 存在并可用于满足 CHV 应用程序 PIN。</li>
<li><strong>60</strong> – 应用程序和全局 Pin 都存在，而且可用于满足 CHV。</li>
</ul>
</dd>
</dl></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfilecontrolparametersdffcpspanspan-idfilecontrolparametersdffcpspanspan-idfilecontrolparametersdffcpspanfile-control-parameters-df-fcp"></a><span id="File_Control_Parameters__DF_FCP_"></span><span id="file_control_parameters__df_fcp_"></span><span id="FILE_CONTROL_PARAMETERS__DF_FCP_"></span>文件控制参数 (DF FCP)

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Tag</th>
<th align="left">Len</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">62</td>
<td align="left">Var。</td>
<td align="left"><p>FCP 模板</p>
<p></p>
<dl>
<dt><span id="Tag"></span><span id="tag"></span><span id="TAG"></span>标记</dt>
<dd><p>82</p>
</dd>
<dt><span id="Len"></span><span id="len"></span><span id="LEN"></span>Len</dt>
<dd><p>01</p>
</dd>
<dt><span id="Value"></span><span id="value"></span><span id="VALUE"></span>值</dt>
<dd><p>文件描述符字节：38 ("不共享-DF")</p>
</dd>
</dl>
<p></p>
<dl>
<dt><span id="Tag"></span><span id="tag"></span><span id="TAG"></span>标记</dt>
<dd><p>8C</p>
</dd>
<dt><span id="Len"></span><span id="len"></span><span id="LEN"></span>Len</dt>
<dd><p>03</p>
</dd>
<dt><span id="Value"></span><span id="value"></span><span id="VALUE"></span>值</dt>
<dd><p>安全特性以紧凑 =</p>
<p>03 30 30</p>
<ul>
<li><strong>40</strong> – 以下字节指定创建文件的 EFs 和删除文件用于 EFs （和要求按该顺序）。</li>
<li><strong>60</strong> – 用户身份验证或外部身份验证满足要求，以创建 EFs。</li>
<li><strong>60</strong> – 用户身份验证或外部身份验证满足要求，以删除 EFs。</li>
</ul>
<div class="alert">
<strong>请注意</strong>  安全属性不具有完全匹配，但允许用户身份验证或外部身份验证，以创建并删除 EFs 不需要。
</div>
<div>
 
</div>
</dd>
</dl></td>
</tr>
</tbody>
</table>

 

一旦创建 DF FCP 后，卡应切换为"初始化"状态，这是创建以下各节中列出的对象所需的状态。

### <a name="span-idpincreationspanspan-idpincreationspanspan-idpincreationspan-pin-creation"></a><span id="_PIN_Creation"></span><span id="_pin_creation"></span><span id="_PIN_CREATION"></span> PIN 创建

若要创建 PIN，应用程序密码更改引用数据 APDU 必须发送到卡：

|            |                              |
|------------|------------------------------|
| CLA        | 00                           |
| INS        | 24                           |
| P1         | 01                           |
| P2         | 80                           |
| Lc         | 命令数据字段的长度 |
| 数据字段 | &lt;password&gt;             |
| le         | 不存在                       |

 

例如，若要设置到 12345678 PIN，以下 APDU 必须发送到卡：

``` syntax
00 24 01 80 08 31 32 33 34 35 36 37 38
```

### <a name="span-idpinunblockkeypukcreationspanspan-idpinunblockkeypukcreationspanspan-idpinunblockkeypukcreationspan-pin-unblock-key-puk-creation"></a><span id="_Pin_Unblock_Key__PUK__Creation"></span><span id="_pin_unblock_key__puk__creation"></span><span id="_PIN_UNBLOCK_KEY__PUK__CREATION"></span> Pin 取消阻止键 (PUK) 创建

PUK 用于取消阻止和/或重置在情况下，卡被阻塞或忘记了 PIN 的 PIN。 如果管理员密钥盘询/响应是改为使用，则不会产生 PUK。

若要创建 PUK，应用程序正在重置密码更改引用数据 APDU 必须发送到卡：

|            |                              |
|------------|------------------------------|
| CLA        | 00                           |
| INS        | 24                           |
| P1         | 01                           |
| P2         | 81                           |
| Lc         | 命令数据字段的长度 |
| 数据字段 | &lt;password&gt;             |
| le         | 不存在                       |

 

例如，若要设置到 12345678 PUK，以下 APDU 必须发送到卡：

``` syntax
00 24 01 81 08 31 32 33 34 35 36 37 38
```

### <a name="span-idaclcreationspanspan-idaclcreationspanspan-idaclcreationspan-acl-creation"></a><span id="_ACL_Creation"></span><span id="_acl_creation"></span><span id="_ACL_CREATION"></span> ACL 创建

必须使用创建文件 APDU 创建 Acl:

|            |                      |
|------------|----------------------|
| CLA        | 00                   |
| INS        | E0                   |
| P1-P2      | 00 00                |
| Lc         | 数据字段的长度 |
| 数据字段 | EF 的 FCP 模板  |
| le         | 不存在               |

 

必须创建下表中所述的 Acl。 每个 ACL 创建 APDU 后面必须跟 ActivateFile APDU (00 44 00 00 00)

| ACL                      | APDU                                                     |
|--------------------------|----------------------------------------------------------|
| UserCreateDeleteDirAc    | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 00 8C 03 03 30 00 |
| EveryoneReadUserWriteAc  | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 10 8C 03 03 30 00 |
| UserWriteExecuteAc       | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 11 8C 03 03 30 FF |
| EveryoneReadAdminWriteAc | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 12 8C 03 03 20 00 |
| UserReadWriteAc          | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 13 8C 03 03 30 30 |
| AdminReadWriteAc         | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 14 8C 03 03 20 20 |

 

### <a name="span-idcreateefforadminkeyspanspan-idcreateefforadminkeyspanspan-idcreateefforadminkeyspan-create-ef-for-admin-key"></a><span id="_Create_EF_for_Admin_Key"></span><span id="_create_ef_for_admin_key"></span><span id="_CREATE_EF_FOR_ADMIN_KEY"></span> 为管理密钥创建 EF

必须使用创建文件 APDU 创建管理密钥的 EF:

|            |                                                |
|------------|------------------------------------------------|
| CLA        | 00                                             |
| INS        | E0                                             |
| P1-P2      | 00 00                                          |
| Lc         | 数据字段的长度                           |
| 数据字段 | EF 的 FCP 模板 (EFID = B080 和 KeyID = 80) |
| le         | 不存在                                         |

 

以下 APDU 必须发送到卡中为三重 DES 三个密钥管理密钥创建 EF:

``` syntax
00 E0 00 00 1C 62 1A 82 01 18 83 02 B0 80 8C 04 87 00 20 FF A5 0B A4 09 80 01 02 83 01 80 95 01 C0
```

上述命令后面必须跟 ActivateFile APDU:

``` syntax
00 44 00 00 00
```

### <a name="span-idinjectadminkeyspanspan-idinjectadminkeyspanspan-idinjectadminkeyspan-inject-admin-key"></a><span id="_Inject_Admin_Key"></span><span id="_inject_admin_key"></span><span id="_INJECT_ADMIN_KEY"></span> 插入管理密钥

管理密钥必须插入到使用 PUT 密钥 APDU 卡：

|            |                      |
|------------|----------------------|
| CLA        | 00                   |
| INS        | DB                   |
| P1-P2      | 3F FF                |
| Lc         | 数据字段的长度 |
| 数据字段 | 密钥用法模板   |
| le         | 不存在               |

 

以下 APDU 必须发送到卡管理员密钥注入 KeyID 80:

``` syntax
00 DB 3F FF 26 70 24 84 01 80 A5 1F 87 18 01 02 03 04 05 06 07 08 01 02 03 04 05 06 07 08 01 02
03 04 05 06 07 08 88 03 B0 73 DC
```

在上面所述的示例中将管理密钥注入具有以下值：

``` syntax
01 02 03 04 05 06 07 08 01 02 03 04 05 06 07 08 01 02 03 04 05 06 07 08
```

### <a name="span-idsetoperationalstatespanspan-idsetoperationalstatespanspan-idsetoperationalstatespan-set-operational-state"></a><span id="__Set_Operational_State"></span><span id="__set_operational_state"></span><span id="__SET_OPERATIONAL_STATE"></span> 设置操作状态

转换从"初始化"状态为"操作"状态，选择与后接 EFID DF 的卡，以便激活文件的命令需要发送到卡。

首先，将选择 APDU 的 DF 发送：

|            |        |
|------------|--------|
| CLA        | 00     |
| INS        | A4     |
| P1-P2      | 00 0C  |
| Lc         | 02     |
| 数据字段 | 3F FF  |
| le         | 不存在 |

 

其次，使用激活文件 APDU DF 将状态更改为"操作":

|            |        |
|------------|--------|
| CLA        | 00     |
| INS        | 44     |
| P1-P2      | 00 00  |
| Lc         | 00     |
| 数据字段 | 不存在 |
| le         | 不存在 |

 

以下 APDU 必须发送到卡中将它放到操作状态：

``` syntax
00 A4 00 0C 02 3F FF
00 44 00 00 00
```

此步骤后，卡已准备好将放置在文件系统规范部分中所述的文件系统，并被视为"空白卡"。 按照卡"创建"将文件系统上使用微型驱动程序 API 的卡的步骤。 此外，按照下一部分，以使用 Apdu 在卡上放置文件系统中的步骤。

### <a name="span-iddataobjectsonagidscardafterthefilesystemiscreatedspanspan-iddataobjectsonagidscardafterthefilesystemiscreatedspanspan-iddataobjectsonagidscardafterthefilesystemiscreatedspan-data-objects-on-a-gids-card-after-the-filesystem-is-created"></a><span id="_Data_objects_on_a_GIDS_card_after_the_filesystem_is_created"></span><span id="_data_objects_on_a_gids_card_after_the_filesystem_is_created"></span><span id="_DATA_OBJECTS_ON_A_GIDS_CARD_AFTER_THE_FILESYSTEM_IS_CREATED"></span> GID 卡后创建文件系统上的数据对象

对于符合与 Microsoft 的泛型配置文件的 GID 规范的卡下, 表描述数据对象和其相应 EFIDs 后在卡"创建"部分所述创建必需的对象。 将每个到卡微型驱动程序 API 不被用于创建文件系统放置数据 APDU 使用 GID 规范中指定下表中的数据对象。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">EFID</th>
<th align="left">标记</th>
<th align="left">目录</th>
<th align="left">友好名称</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">A000</td>
<td align="left">DF1F</td>
<td align="left"><pre class="syntax" space="preserve"><code>01 6d 73 63 70 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 a0 00 00 00 00 00
00 00 00 00 00 00 63 61 72 64 69 64 00 00 00 00
00 20 df 00 00 12 a0 00 00 00 00 00 00 00 00 00
00 00 63 61 72 64 61 70 70 73 00 00 00 21 df 00
00 10 a0 00 00 00 00 00 00 00 00 00 00 00 63 61
72 64 63 66 00 00 00 00 00 22 df 00 00 10 a0 00
00 6d 73 63 70 00 00 00 00 00 63 6d 61 70 66 69
6c 65 00 00 00 23 df 00 00 10 a0 00 00</code></pre></td>
<td align="left">主文件系统表</td>
</tr>
<tr class="even">
<td align="left">A010</td>
<td align="left">DF21</td>
<td align="left"><pre class="syntax" space="preserve"><code>6d 73 63 70 00 00 00 00</code></pre></td>
<td align="left">\cardapps</td>
</tr>
<tr class="odd">
<td align="left">A010</td>
<td align="left">DF22</td>
<td align="left"><pre class="syntax" space="preserve"><code>00 00 00 00 00 00</code></pre></td>
<td align="left">\cardcf</td>
</tr>
<tr class="even">
<td align="left">A010</td>
<td align="left">DF23</td>
<td align="left"><pre class="syntax" space="preserve"><code>&lt;empty 0-byte data object&gt;</code></pre></td>
<td align="left">mscp\cmapfile</td>
</tr>
<tr class="odd">
<td align="left">A012</td>
<td align="left">DF20</td>
<td align="left"><pre class="syntax" space="preserve"><code>&lt;random 16-byte value&gt;</code></pre></td>
<td align="left">\cardid</td>
</tr>
</tbody>
</table>

 

## <a name="span-idinfsampletore-brandinboxclassminidriverspanspan-idinfsampletore-brandinboxclassminidriverspanspan-idinfsampletore-brandinboxclassminidriverspaninf-sample-to-re-brand-inbox-class-minidriver"></a><span id="INF_Sample_to_re-brand_inbox_class_minidriver"></span><span id="inf_sample_to_re-brand_inbox_class_minidriver"></span><span id="INF_SAMPLE_TO_RE-BRAND_INBOX_CLASS_MINIDRIVER"></span>为重新标记收件箱类微型驱动程序 INF 示例


智能卡供应商可以使用收件箱微型驱动程序而无需将传送一个驱动程序包。 若要将品牌信息添加到此类卡插体验，供应商可以提供重写各种字符串，以便提供品牌信息的 INF 文件。 这些字符串如下所示：

-   ProviderName
-   CardDeviceName
-   SmartCardName

下面是一个示例 INF 文件，可以在收件箱微型驱动程序。 此 INF 文件安装在 x86 和 amd64 CPU 平台进行了修饰。

``` syntax
;
;FabrikamVendor Smartcard Minidriver for an x86 and x64 based package.
;

[Version]
Signature="$Windows NT$"
Class=SmartCard
ClassGuid={990A2BD7-E738-46c7-B26F-1CF8FB9F1391}
Provider=%ProviderName%
CatalogFile=delta.cat
DriverVer=10/03/2009,10.0.0.1

[Manufacturer]
%ProviderName%=Minidriver,NTamd64,NTamd64.6.1,NTx86,NTx86.6.1

[Minidriver.NTamd64]
%CardDeviceName%=Minidriver64_Install,SCFILTER\CID_51FF0800

[Minidriver.NTx86]
%CardDeviceName%=Minidriver32_Install,SCFILTER\CID_51FF0800

[Minidriver.NTamd64.6.1]
%CardDeviceName%=Minidriver64_61_Install,SCFILTER\CID_51FF0800

[Minidriver.NTx86.6.1]
%CardDeviceName%=Minidriver32_61_Install,SCFILTER\CID_51FF0800

[DefaultInstall]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault

[DefaultInstall.ntamd64]
CopyFiles=amd64_CopyFiles
CopyFiles=wow64_CopyFiles
AddReg=AddRegWOW64
AddReg=AddRegDefault

[DefaultInstall.NTx86]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault

[DefaultInstall.ntamd64.6.1]
AddReg=AddRegWOW64
AddReg=AddRegDefault

[DefaultInstall.NTx86.6.1]
AddReg=AddRegDefault

[SourceDisksFiles]
msclmd64.dll=1
msclmd.dll=1

[SourceDisksNames]
1 = %MediaDescription%

[Minidriver64_Install.NT]
CopyFiles=amd64_CopyFiles
CopyFiles=wow64_CopyFiles
AddReg=AddRegWOW64
AddReg=AddRegDefault

[Minidriver64_61_Install.NT]
AddReg=AddRegWOW64
AddReg=AddRegDefault
Include=umpass.inf
Needs=UmPass

[Minidriver32_Install.NT]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault

[Minidriver32_61_Install.NT]
AddReg=AddRegDefault
Include=umpass.inf
Needs=UmPass

[Minidriver64_61_Install.NT.Services]
Include=umpass.inf
Needs=UmPass.Services

[Minidriver32_61_Install.NT.Services]
Include=umpass.inf
Needs=UmPass.Services


[Minidriver64_61_Install.NT.HW]
Include=umpass.inf
Needs=UmPass.HW

[Minidriver64_61_Install.NT.CoInstallers]
Include=umpass.inf
Needs=UmPass.CoInstallers


[Minidriver64_61_Install.NT.Interfaces]
Include=umpass.inf
Needs=UmPass.Interfaces


[Minidriver32_61_Install.NT.HW]
Include=umpass.inf
Needs=UmPass.HW

[Minidriver32_61_Install.NT.CoInstallers]
Include=umpass.inf
Needs=UmPass.CoInstallers


[Minidriver32_61_Install.NT.Interfaces]
Include=umpass.inf
Needs=UmPass.Interfaces


[amd64_CopyFiles]
msclmd.dll,msclmd64.dll

[x86_CopyFiles]
msclmd.dll

[wow64_CopyFiles]
msclmd.dll

[AddRegWOW64]
HKLM, %SmartCardNameWOW64%,"ATR",0x00000001,3b,04,51,ff,08,00
HKLM, %SmartCardNameWOW64%,"ATRMask",0x00000001,ff,ff,ff,ff,ff,ff
HKLM, %SmartCardNameWOW64%,"Crypto Provider",0x00000000,"Microsoft Base Smart Card Crypto Provider"
HKLM, %SmartCardNameWOW64%,"Smart Card Key Storage Provider",0x00000000,"Microsoft Smart Card Key Storage Provider"
HKLM, %SmartCardNameWOW64%,"80000001",0x00000000,%SmartCardCardModule%

[AddRegDefault]
HKLM, %SmartCardName%,"ATR",0x00000001,3b,04,51,ff,08,00
HKLM, %SmartCardName%,"ATRMask",0x00000001,ff,ff,ff,ff,ff,ff
HKLM, %SmartCardName%,"Crypto Provider",0x00000000,"Microsoft Base Smart Card Crypto Provider"
HKLM, %SmartCardName%,"Smart Card Key Storage Provider",0x00000000,"Microsoft Smart Card Key Storage Provider"
HKLM, %SmartCardName%,"80000001",0x00000000,%SmartCardCardModule%

[DestinationDirs]
amd64_CopyFiles=10,system32
x86_CopyFiles=10,system32
wow64_CopyFiles=10,syswow64


; =================== Generic ==================================

[Strings]
ProviderName ="FabrikamVendor"
MediaDescription="FabrikamVendor Smart Card Minidriver Installation Disk"
CardDeviceName="FabrikamVendor Minidriver for Smart Card"
SmartCardName="SOFTWARE\Microsoft\Cryptography\Calais\SmartCards\Fabrikam"
SmartCardNameWOW64="SOFTWARE\Wow6432Node\Microsoft\Cryptography\Calais\SmartCards\Fabrikam"
SmartCardCardModule="msclmd.dll"
```

此类型的 INF 文件需要以下项：

-   由 %fabrikamcarddevicename%字符串必须 ATR 历史字节的设备或设备的智能卡框架标识符的已解码的值指定硬件 ID。 有关此标识符的详细信息，请参阅中的"Windows 智能卡框架卡标识符"一节[发现过程](discovery-process.md)。
-   **DefaultInstall**部分是必需的智能卡微型驱动程序的包的 INF 文件中。
-   **DriverVer** INF 文件中的指令必须具有一个值，大于收件箱驱动程序的 INF 文件中的版本和时间戳值。 否则，系统不安装使用供应商的 INF 文件设备。

    **DriverVer**指令具有以下语法。

    ``` syntax
    DriverVer=mm/dd/yyyy[,w.x.y.z]
    ```

    我们建议设置的值时请遵循以下准则**DriverVer**指令：

    -   指定一个日期值，是足够遥远的将来以避免与 Windows service pack 更新冲突。
    -   尽管 4 位版本号是可选的但必须指定明显高于收件箱驱动程序的 INF 文件中指定的当前版本的版本。

INF 文件和语法的详细信息，请参阅[设备和驱动程序安装设计指南](https://msdn.microsoft.com/library/windows/hardware/ff549455)。

 

 





